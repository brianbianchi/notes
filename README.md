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