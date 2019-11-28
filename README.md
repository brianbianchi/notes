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