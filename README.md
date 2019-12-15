# Algorithms

1. Depth First Search
2. Breadth First Search
3. Matching Parenthesis problem
4. Using Hash Tables
5. Variables/Pointers manipulation
6. reverse linked list (duplicates , removing duplicates)
7. Sorting fundamentals (quick sort, merge sort, bubble sort,
   runtime of a sort, time space complexity)
8. Recursion
9. Custom data structures (object oriented programming)
10. Binary search

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


</details>

<details>
<summary>SQL injection</summary>


</details>

<details>
<summary>Cross site scripting (XSS)</summary>


</details>

# SQL

<details>
<summary>SQL transactions</summary>


</details>

# VIM

<details>
<summary>Cheat sheet</summary>


</details>

# Object oriented programming

<details>
<summary>C# keywords</summary>


</details>