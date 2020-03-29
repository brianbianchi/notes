# Algorithms

<details>
<summary>[Depth First Search](https://en.wikipedia.org/wiki/Depth-first_search)</summary>
</details>
<details>
<summary>[Breadth First Search](https://en.wikipedia.org/wiki/Breadth-first_search)</summary>
</details>
<details>
<summary>[Matching Parenthesis problem](https://www.geeksforgeeks.org/check-for-balanced-parentheses-in-an-expression/)</summary>
</details>
<details>
<summary>[Hash Tables](https://en.wikipedia.org/wiki/Hash_table)</summary>
</details>
<details>
<summary>[Variables/Pointers manipulation](https://en.wikipedia.org/wiki/Pointer_(computer_programming))</summary>
</details>
<details>
<summary>[reverse linked list (duplicates , removing duplicates)](https://en.wikipedia.org/wiki/Linked_list)</summary>
</details>
<details>
<summary>[Sorting fundamentals (quick sort, merge sort, bubble sort,runtime of a sort, time space complexity)](https://en.wikipedia.org/wiki/Sorting_algorithm)</summary>
</details>
<details>
<summary>[Recursion](https://en.wikipedia.org/wiki/Recursion)</summary>
</details>
<details>
<summary>[Custom data structures (object oriented programming)](https://en.wikipedia.org/wiki/Object-oriented_programming)</summary>
</details>
<details>
<summary>[Binary search](https://en.wikipedia.org/wiki/Binary_search_algorithm)</summary>
</details>

# SOLID principals

<details>
<summary>Single-responsibility principle (SRP)</summary>

A class should only have a single responsibility. This simply means only changes to one part of the software’s specification should be able to affect the specification of the class.

```java
public class PaymentProcessing
{
    public void Process(object obj)
    {
         //process logic here
    }
}
```

This class abides by the single-responsibility principle because it only does one thing and that is to process payment. If we were to add a method that does something other than processing payment, then that would violate the single-responsibility principle. The reason being is because that class would now have multiple responsibilities. Let’s say we wanted to also process Discounts in concert in payments. You might be tempted to just add the logic to process discounts in the PaymentProcessing class. But payment processing and applying discounts to payment are two different things. The solution would be to change our payment class to return the processed payment object, then create a separate Discount class, then hand over the processed payment as a parameter to the Discount class. That way the payment class still has one responsibility and now we have a Discount class that only applies discounts to processed payments. A change to the Discount class wouldn’t affect the PaymentProcessing class and vice versa.

</details>

<details>
<summary>Open-closed principle (OCP)</summary>

A class should be extendable, but closed to modification. That simply means any desired additional behavior should be added to another class that extends your original class instead of modifying it.

```java
public class Vehicle
{
    public string Make { get; set; }
    public string Model { get; set; }
    public string Trim { get; set; }
    public string Year { get; set; }
    public string Color { get; set; }
    //vehicle related logic goes here
}
```

After implementing all the required functionalities, you find out a month later that there’s a Luxury type of vehicle that shares the same functionalities as your Vehicle class except for some added premium options. Modifying the vehicle class is not the right way to solve that issue. That would violate the open-closed principle. The way to solve the issue is to extend the Vehicle class and add the additional functionalities in your new class.

```java
public class LuxuryVehicle : Vehicle
{
    public List<string> AdditionalOptions { get; set; }
    //luxury vehicle related logic goes here
}
```

By extending the Vehicle class, we inherit all the functionalities and we’re free to add whatever luxury-related logic in our new class without any fear of breaking existing functionality.

</details>

<details>
<summary>Liskov substitution principle (LSP)</summary>

A derived class must be substitutable for its base class.

Using the example code from earlier, we must be able to swap our LuxuryVehice class for our Vehicle class with no issue. Supposed we add a new property to our base class named MSRP and add a new method call `getHalfPrice()`. All this method does is dividing the MSRP value by 2. The base class precondition is that the property value will always be greater than zero.

A few weeks after bragging about how awesome your Vehicle class is, you receive new requirements that allow the MSRP in your LuxuryVehicle class to be zero with added premium options. The new requirements violate the Liskov substitution principle. A way to solve that would be to create an interface for each of the vehicle classes with the appropriate method signatures. The vehicle class would have the `getHalfPrice()` method, then the LuxuryVehicle could have the `getZeroMSRPPriceWithAddedOption()`.

</details>

<details>
<summary>Interface segregation principle (ISP)</summary>

Client-specific interfaces are better than one general-purpose interface.

Let’s say we had an interface called Staff, which would have methods such as teach, clean, processPayment, advise, etc… If we were to create a Professor class, we’d have to implement all these methods even though some of them are not related to being a professor. This interface violates the Interface segregation principle.

The solution would be to create client-specific interfaces such as _Professor, Administrator, GuidanceCounselor, Janitor, etc..._ Each interface would have the appropriate method.
* Professor -> `teach()`
* Administrator -> `processPayment()`
* GuidanceCounselor -> `advise()`
* Janitor -> `clean()`

Because of this fined grained approach, now clients can choose which one suits their specific needs. They wouldn’t have to implement method they don’t need.

</details>

<details>
<summary>Dependency inversion Principle (DIP)</summary>

The high-level module must not depend on the low-level module, but they should depend on abstractions.

```java
public class MessageBoard
{
    private WhatUpMessage message;
    public MessageBoard(WhatsUpMessage message)
    {
        this.message = message;
    }
}
```

The high-level module MessageBoard now depends on the low-level WhatsUpMessage. If we needed to print the underlying message in the high-level module, we would now find ourselves at the mercy of the low-level module. We would have to write WhatsUpMessage specific logic to print that message. If later, FacebookMessage needed to be supported, we would have to modify the high-level module( tightly-coupled code). That violates the Dependency inversion principle.

A way to fix that would be to extract that dependency. Create an interface and add whatever your high-level module needs. Any class that needed to use your high-level module would have to implement that interface.

Your interface would look something like this

```java
public interface IMessage
{
   public void PrintMessage();
}
```

Your MessageBoard now would look like this

```java
public class MessageBoard
{
    private IMessage message;
    public MessageBoard(IMessage message)
    {
        this.message = message;
    }
    public void PrintMessage()
    {
        this.message.PrintMessage();
    }
}
```

The low-level module would look like this

```java
public class WhatUpMessage : IMessage
{
    public void PrintMessage()
    {
        //print whatsup message
    }
}
public class FacebookMessage : IMessage
{
    public void PrintMessage()
    {
        //print facebook message
    }
}
```

That abstraction removes the dependency of the low-level module in your high-level module. The high-level module is now completely independent of any low-level module.

</details>

# Security

<details>
<summary>Clickjacking</summary>

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

</details>

<details>
<summary>Command execution</summary>

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

</details>

<details>
<summary>SQL injection</summary>

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

</details>

<details>
<summary>Cross site scripting (XSS)</summary>

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

</details>

# SQL

<details>
<summary>SQL transactions</summary>

One way to safely make changes to your SQL database is by using `transactions`. By wrapping statements in a transaction, you are able to revert your changes, if needed.

### Example
In this example, I wrap a couple of delete statements in a transaction.

```sql
BEGIN tran
SAVE tran point1

DELETE FROM table
WHERE var = 2
SAVE tran point2

DELETE FROM table
WHERE var = 3
SAVE tran point3
```

If you need to revert your changes, `rollback` to a save point.

```sql
rollback tran point1
```

</details>

# VIM

<details>
<summary>Cheat sheet</summary>

Vim is a powerful text editor that is useful to programmers, system administrators, and heavy editors of plain text files. You are likely to first experience Vim on a linux system or when trying to resolve code conflicts using git. After you read this post, I recommend that you go through the interactive tutorial by typing `vimtutor` into your command line.

The command to edit a file using Vim is `vim filename.type`. There are three main modes to Vim: insert, command, and last-line.

### Command Mode `esc`
When first entering Vim, you begin in command mode. This means that all alphanumeric keys are bound to commands, rather than inserting respective characters.
#### Movements

`h` - one character to the left

`j` - down one line

`k` - up one line

`l` - one character to the right

`0` - to the beginning of the line

`$` - to the end of the line

`w` - forward one word

`b` - backward one word

`G` - to the end of the file

`gg` - to the beginning of the file

`` `. ``  - to the last edit

Prefacing a movement with a number will execute the command that many times. For example, `4j` will move your cursor down four lines.

#### Editing
`x` - delete character

`dw` - deletes from cursor to end of word

`d0` - delete to beginning of a line

`d$` - delete to end of a line

`dgg` - delete to beginning of file

`dG` - delete to end of file

`u` - undo last operation(s)

`Ctrl-r` - redo last undo(s)

#### Search and Replace
`/text` - search for "text", going forward

`n` - move cursor to next instance of searched text (wrapped at end of document)

`N` - move cursor to previous instance of searched text

`?text` - search for "text", going backward

`:%s/text/replacement/g` - search entire document and replace "text" with "replacement"

`:%s/text/replacement/gc` - search entire document and replace "text" with "replacement", with confirmation

#### Copying and Pasting
The last bit of text you deleted is now in your buffer and is ready to be pasted.

`p` - paste text after current line

`P` - paste text on current line

`v` - highlight one character at a time

`V` - highlight one line at a time

`Ctrl-v` - highlight by column

`y` - yank text, after highlighting, place into buffer

### Insert Mode `i`
This mode allows you to insert the respective characters you type on your keyboard. To go back to command mode, use `esc`.

### Last-line Mode `:`
`:q` - quit the editor

`:q!` - override save and quit

`:w {filename}` - write (save) the file

`:ZZ` - save and quit

</details>

# Object oriented programming

<details>
<summary>C# keywords</summary>

This post is a collection of important C# keyword definitions. Many of these descriptions are from the [Microsoft docs](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/).

### static
The static modifier is used to declare a static member, which belongs to the type itself rather than to a specific object. The static modifier can be used with classes, fields, methods, properties, operators, events, and constructors.

```cs
public class MyBaseC
{
    public struct MyStruct
    {
        public static int x = 100;
    }
}
```

### abstract class
The abstract modifier indicates that the thing being modified has a missing or incomplete implementation. The abstract modifier can be used with classes, methods, properties, indexers, and events. Members marked as abstract, or included in an abstract class, must be implemented by classes that derive from the abstract class. The `override` modifier is required to extend or modify the abstract or virtual implementation of an inherited method, property, indexer, or event.

```cs
abstract class ShapesClass
{
    abstract public int Area();
}
class Square : ShapesClass
{
    int side = 0;

    public Square(int n)
    {
        side = n;
    }
    // Area method is required to avoid
    // a compile-time error.
    public override int Area()
    {
        return side * side;
    }

    static void Main() 
    {
        Square sq = new Square(12);
        Console.WriteLine("Area of the square = {0}", sq.Area()); // 144s
    }

    interface I
    {
        void M();
    }
    abstract class C : I
    {
        public abstract void M();
    }

}
```

### virtual
The virtual keyword is used to modify a method, property, indexer, or event declaration and allow for it to be overridden in a derived class. The `override` modifier is required to extend or modify the abstract or virtual implementation of an inherited method, property, indexer, or event.

```cs
class MyBaseClass
{
    // virtual auto-implemented property. Overrides can only
    // provide specialized behavior if they implement get and set accessors.
    public virtual string Name { get; set; }

    // ordinary virtual property with backing field
    private int num;
    public virtual int Number
    {
        get { return num; }
        set { num = value; }
    }
}


class MyDerivedClass : MyBaseClass
{
    private string name;

   // Override auto-implemented property with ordinary property
   // to provide specialized accessor behavior.
    public override string Name
    {
        get
        {
            return name;
        }
        set
        {
            if (value != String.Empty)
            {
                name = value;
            }
            else
            {
                name = "Unknown";
            }
        }
    }

}
```

### interface
An interface contains only the signatures of methods, properties, events or indexers. A class or struct that implements the interface must implement the members of the interface that are specified in the interface definition.

```cs
interface ISampleInterface
{
    void SampleMethod();
}

class ImplementationClass : ISampleInterface
{
    // Explicit interface member implementation: 
    void ISampleInterface.SampleMethod()
    {
        // Method implementation.
    }

    static void Main()
    {
        // Declare an interface instance.
        ISampleInterface obj = new ImplementationClass();

        // Call the member.
        obj.SampleMethod();
    }
}
```

### sealed
When applied to a class, the sealed modifier prevents other classes from inheriting from it. In the following example, class B inherits from class A, but no class can inherit from class B.

```cs
class A {}      
sealed class B : A {}  
```

### struct
A struct type is a value type that is typically used to encapsulate small groups of related variables, such as the coordinates of a rectangle or the characteristics of an item in an inventory. 

```cs
public struct Book  
{  
    public decimal price;  
    public string title;  
    public string author;  
}  
```

### delegate
A delegate is a type that represents references to methods with a particular parameter list and return type. When you instantiate a delegate, you can associate its instance with any method with a compatible signature and return type. You can invoke (or call) the method through the delegate instance.

Delegates are used to pass methods as arguments to other methods. Event handlers are nothing more than methods that are invoked through delegates. You create a custom method, and a class such as a windows control can call your method when a certain event occurs.

```cs
public delegate int PerformCalculation(int x, int y);
```

### params
By using the params keyword, you can specify a method parameter that takes a variable number of arguments.

```cs
public class MyClass
{
    public static void UseParams(params int[] list)
    {
        for (int i = 0; i < list.Length; i++)
        {
            Console.Write(list[i] + " ");
        }
        Console.WriteLine();
    }
}
```

### ref
The ref keyword indicates a value that is passed by reference. It is used in four different contexts:

* In a method signature and in a method call, to pass an argument to a method by reference. See Passing an argument by reference for more information.
* In a method signature, to return a value to the caller by reference. See Reference return values for more information.
* In a member body, to indicate that a reference return value is stored locally as a reference that the caller intends to modify or, in general, a local variable accesses another value by reference. See Ref locals for more information.
* In a struct declaration to declare a ref struct or a ref readonly struct. See ref struct declarations for more information.

```cs
void Method(ref int refArgument)
{
    refArgument = refArgument + 44;
}

int number = 1;
Method(ref number);
Console.WriteLine(number); // 45
```

### out 
The out keyword causes arguments to be passed by reference. It is like the ref keyword, except that ref requires that the variable be initialized before it is passed. It is also like the in keyword, except that in does not allow the called method to modify the argument value. To use an out parameter, both the method definition and the calling method must explicitly use the out keyword.

```cs
int initializeInMethod;
OutArgExample(out initializeInMethod);
Console.WriteLine(initializeInMethod);     // 44

void OutArgExample(out int number)
{
    number = 44;
}
```

</details>
