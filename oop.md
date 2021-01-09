# Object oriented programming

## C# keywords</summary>

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
