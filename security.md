# Security

## Clickjacking

*Clickjacking* is a method that tricks users into clicking on harmful links, by disguising the link as something else. Attackers can do this by building their own site with a similar domain to a popular site, including the popular site using an [iframe](https://www.w3schools.com/tags/tag_iframe.asp), and adding a transparent div, wrapped by a link tag, over the iframe. The div can be placed over the iframe by setting its [z-index](https://www.w3schools.com/cssref/pr_pos_z-index.asp) to a value higher than the iframe's z-index. The link can be used to download malware or direct the user to another site.

Clickjacking has been used to do the following:

* collect login credentials
  * render a fake login box on top of the real one
* trick users into turning on their web-cam or microphone
  * render invisible elements over the Adobe Flash settings page
* spread worms on social media sites
* promote online scams by tricking people into clicking on a link
* spread malware by diverting users to malicious download links

### Protection

To ensure that your site doesn’t get targeted by a clickjacking attack, you need to make sure it cannot be wrapped in an iframe. This can be done by giving the browser instructions directly via HTTP headers, or by using client-side JavaScript for older browsers (also known as frame-killing).

##### X-Frame-Options

The `X-Frame-Options` HTTP header can be used to indicate whether or not a browser should be allowed to render a page in a `<frame>`, `<iframe>` or `<object>` tag. It was designed specifically to help protect against clickjacking.

There are three permitted values for the header:

* DENY - The page cannot be displayed in a frame, regardless of the site attempting to do so.
* SAMEORIGIN - The page can only be displayed in a frame on the same origin as the page itself.
* ALLOW-FROM *uri* - The page can only be displayed in a frame on the specified origins.

##### Content Security Policy

The `Content-Security-Policy` HTTP header is part of the HTML5 standard. This header replaces and provides a broader range of protection than the `X-Frame-Options` header. It is designed in such a way that website authors can whitelist individual domains from which resources (like scripts, stylesheets, and fonts) can be loaded.

To control where your site can be embedded, use the frame-ancestors directive:

`Content-Security-Policy: frame-ancestors 'none'` cannot be displayed in a frame, regardless of the site attempting to do so.

`Content-Security-Policy: frame-ancestors 'self'` can only be displayed in a frame on the same origin as the page itself.

`Content-Security-Policy: frame-ancestors *uri*` can only be displayed in a frame on the specified origins.

##### Frame-Killing

In older browsers, the most common way to protect users against clickjacking was to include frame-killing JavaScript to prevent the page from being included in iframes:

```html
<style>
  /* Hide page by default */
  html { display : none; }
</style>

<script>
  if (self == top) {
    // Everything checks out, show the page
    document.documentElement.style.display = 'block';
  } else {
    // Break out of the frame
    top.location = self.location;
  }
</script>
```

When the page loads, this code will check that the domain of the page matches the domain of the browser window, which will not be true when the page is embedded in an iframe.

## Command execution

If your web application calls operating system processes via the command line, an attacker may be able to execute arbitrary code on your server. This type of attack is coined *command execution*.  

Remote code execution can allow attackers to gaining access to the server, escalate their user privileges, install malicious scripts, or make your server part of a botnet to be used at a later date.

### Protection

If your application calls out to the operating system, you need to be sure command strings are constructed securely.

##### Try to Avoid Command Line Calls Altogether

Modern programming languages have interfaces that permit you to read files, send emails, and perform other operation system functions. Use APIs wherever possible and only use shell commands where they are necessary.

###### Escape Inputs Correctly

Injection vulnerabilities occur when untrusted input is not sanitized correctly. If you use shell commands, be sure to scrub input values for potentially malicious characters, such as `;`, `&`, `|`, and `` ` ``. You can also restrict input by testing it against a regular expression of known safe characters (for example, alphanumeric characters).

##### Restrict the Permitted Commands

Try to construct all or most of your shell commands using string literals, rather than user input. Where user input is required, try to whitelist permitted values, or enumerate them in a conditional statement.


## SQL injection

The most common website vulnerability, also known as *SQL injection*, enables attackers to run arbitrary commands against your database, potentially exposing sensitive information.

### Example
Say we enter the below credentials into a login.

username: `user@email.com`

password; `password'`

```bash
An error occurred: PG::SyntaxError: ERROR: unterminated quoted string at or near "'password'' limit 1" LINE 1: ...ers where email = 'user@email.com' and password = 'password'... ^ : select * from users where email = 'user@email.com' and password = 'password'' limit 1.
Unable to login this user due to unexpected error.`
```

This example server log shows a SQL syntax error, indicating that the quote character unexpectedly broke the server logic.

```sql
SELECT *
  FROM users
 WHERE email = 'user@email.com'
   AND pass  = 'password'' LIMIT 1
```

The single quote is directly entered into the SQL string, and terminates the query early. This is what caused the syntax error in the above log, and shows that this application is vulnerable to SQL injection.

An attacker might use the following credentials to gain access to the `username@email.com` account.

username: `username@email.com`

password: `' or 1=1--`

The characters `--` comment out the rest of the SQL statement, causing the database to ignore `LIMIT 1` and the extra single quote. The SQL statement becomes `'' or 1=1`, evaluating to true, which allows the attacker to authenticate without supplying the actual password.

```sql
SELECT *
  FROM users
 WHERE email = 'user@email.com'
   AND pass  = '' or 1=1--' LIMIT 1
```

### Risks
SQL injection attacks can be used to:

* bypass authentication, as shown in the above example
* extract sensitive information, such as passwords, credit card numbers, or SSNs
* delete data or drop tables
* inject malicious code to execute when other users visit the site

### Protection
##### Parameterized Statements
Programming languages talk to SQL databases using drivers. Drivers allow the application to construct and run SQL statements against the database. *Parameterized statements* make sure inputs, inserted into SQL statements, are safe and will no allow attackers to run arbitrary code against your database.

`Secure` way of running SQL query in JDBC:
```java
// Define which user we want to find.
String email = "user@email.com";

// Connect to the database.
Connection conn = DriverManager.getConnection(URL, USER, PASS);
Statement stmt = conn.createStatement();

// Construct the SQL statement we want to run with parameter.
String sql = "SELECT * FROM users WHERE email = ?";

// Run the query, passing the 'email' parameter value.
ResultSet results = stmt.executeQuery(sql, email);

while (results.next()) {
  // Do something with the data returned.
}
```

`Dangerous`, explicit way of running SQL query in JDBC:
```java
// Define which user we want to find.
String email = "user@email.com";

// Connect to the database.
Connection conn = DriverManager.getConnection(URL, USER, PASS);
Statement stmt = conn.createStatement();

// Dangerous way of constructing a query; using string concatenation.
String sql = "SELECT * FROM users WHERE email = '" + email + "'";

// Run the query without parameterizing the input.
ResultSet results = stmt.executeQuery(sql);

while (results.next()) {
  // Hacked.
}
```

The key difference is the input data being passed into the `executeQuery()` [method](https://docs.oracle.com/javase/tutorial/jdbc/basics/processingsqlstatements.html), rather than being concatenated into the SQL query. In the first case, the parameterized string and the parameters are passed to the database separately, which allows the driver to correctly interpret them. In the second case, the full SQL statement is constructed before the driver is invoked, meaning we are vulnerable to maliciously crafted parameters.

If you are unable to use parameterized statements or a library that writes SQL for you, you should make sure to escape special string characters in input parameters. Sanitizing inputs should check that supplied fields like email addresses match a regular expression, ensure that numeric or alphanumeric fields do not contain symbol characters, and reject (or strip)  whitespace and new line characters where they are not appropriate.

Injection attacks often rely on the attacker being able to craft an input that will prematurely close the argument string in which they appear in the SQL statement. Programming languages have standard ways to describe strings containing quotes within them. Typically, doubling up the quote character, replacing `'` with `''`, will treat this quote as part of the string, not the end of the string.

## Cross site scripting (XSS)

Cross Site Scripting (XSS) takes advantage of sites who allow users to add content. XSS allows arbitrary execution of JavaScript code. The damage that can be done by an attacker depends on the sensitivity of the data being handled by your site. Hackers who have exploited XSS have been able to do the following:

* Spread worms on social media sites
* Session hijacking
  * Send the session ID to a remote site under the hacker’s control, allowing the hacker to impersonate that user by hijacking a session in progress
* Identity theft
  * Steal confidential information such as credit card numbers on a compromised site
* Denial of service attacks and website vandalism
* Theft of sensitive data, such as passwords
* Financial fraud on banking sites

### Protection

To protect against stored XSS attacks, make sure any dynamic content coming from the data store cannot be used to inject JavaScript on a page.

##### Escape Dynamic Content

Web pages are usually created by template files, which are made up of HTML mixed with dynamic content. Stored XSS attacks make use of the improper treatment of dynamic content coming from a backend data store. The attacker abuses an editable field by inserting some JavaScript code, which is evaluated in the browser when another user visits that page.

Unless your site is a content-management system, it is rare that you want your users to author raw HTML. Instead, you should escape all dynamic content coming from a data store, so the browser knows it is to be treated as the contents of HTML tags, as opposed to raw HTML.

Escaping dynamic contents generally consists of replacing significant characters with the HTML entity encoding:

`"`	&#34

`#`	&#35

`&`	&#38

`'`	&#39

`(`	&#40

`)`	&#41

`/`	&#47

`;`	&#59

`<`	&#60

`>`	&#62

Most modern frameworks will escape dynamic content by default. Escaping editable content in this way means it will never be treated as executable code by the browser.

##### Whitelist Values

If a particular dynamic data item can only take a handful of valid values, the best practice is to restrict the values in the data store, and have your rendering logic only permit known good values. For instance, instead of asking a user to type in their country of residence, have them select from a drop-down list.

##### Implement Content-Security-Policy

Modern browsers support [Content-Security-Policy](https://developers.google.com/web/fundamentals/security/csp/), which allows the author to control where the site's JavaScript (and other resources) can be loaded and executed from. XSS attacks rely on the attacker being able to run malicious scripts on a user’s web page - either by injecting inline `<script>` tags somewhere within the `<html>` tag of a page, or by tricking the browser into loading the JavaScript from a malicious third-party domain.

By setting a content security policy in the response header, you can tell the browser to never execute inline JavaScript, and to lock down which domains can host JavaScript for a page.

`<meta http-equiv="Content-Security-Policy" content="script-src 'self' https://apis.google.com">`

By whitelisting the URIs from which scripts can be loaded, you are implicitly stating that inline JavaScript is not allowed.
