# Types and members

## Classes and objects

Classes are the most fundamental of C#’s types. A class is a data structure that combines state (fields) and actions (methods and other function members) in a single unit. A class provides a definition for instances of the class, also known as objects. Classes support inheritance and polymorphism, mechanisms whereby derived classes can extend and specialize base classes.

New classes are created using class declarations. A class declaration starts with a header. The header specifies:

The attributes and modifiers of the class
The name of the class
The base class (when inheriting from a base class)
The interfaces implemented by the class.
The header is followed by the class body, which consists of a list of member declarations written between the delimiters { and }.

The following code shows a declaration of a simple class named Point:

```C#
//Copy
public class Point
{
    public int X { get; }
    public int Y { get; }

    public Point(int x, int y) => (X, Y) = (x, y);
}
```

Instances of classes are created using the new operator, which allocates memory for a new instance, invokes a constructor to initialize the instance, and returns a reference to the instance. The following statements create two Point objects and store references to those objects in two variables:

```C#
//Copy
var p1 = new Point(0, 0);
var p2 = new Point(10, 20);

```

The memory occupied by an object is automatically reclaimed when the object is no longer reachable. It's neither necessary nor possible to explicitly deallocate objects in C#.

Type parameters
Generic classes define type parameters. Type parameters are a list of type parameter names enclosed in angle brackets. Type parameters follow the class name. The type parameters can then be used in the body of the class declarations to define the members of the class. In the following example, the type parameters of Pair are TFirst and TSecond:

```C#
//Copy
public class Pair<TFirst, TSecond>
{
    public TFirst First { get; }
    public TSecond Second { get; }

    public Pair(TFirst first, TSecond second) =>
        (First, Second) = (first, second);
}
```

A class type that is declared to take type parameters is called a generic class type. Struct, interface, and delegate types can also be generic. When the generic class is used, type arguments must be provided for each of the type parameters:

```C#
//Copy
var pair = new Pair<int, string>(1, "two");
int i = pair.First;     // TFirst int
string s = pair.Second; // TSecond string
```

A generic type with type arguments provided, like `Pair<int,string>` above, is called a constructed type.

# Base classes

A class declaration may specify a base class. Follow the class name and type parameters with a colon and the name of the base class. Omitting a base class specification is the same as deriving from type object. In the following example, the base class of Point3D is Point. From the first example, the base class of Point is object:

```C#
//Copy
public class Point3D : Point
{
    public int Z { get; set; }

    public Point3D(int x, int y, int z) : base(x, y)
    {
        Z = z;
    }
}
```

A class inherits the members of its base class. Inheritance means that a class implicitly contains almost all members of its base class. A class doesn't inherit the instance and static constructors, and the finalizer. A derived class can add new members to those members it inherits, but it can't remove the definition of an inherited member. In the previous example, Point3D inherits the X and Y members from Point, and every Point3D instance contains three properties, X, Y, and Z.

An implicit conversion exists from a class type to any of its base class types. A variable of a class type can reference an instance of that class or an instance of any derived class. For example, given the previous class declarations, a variable of type Point can reference either a Point or a Point3D:

```C#
//Copy
Point a = new Point(10, 20);
Point b = new Point3D(10, 20, 30);
```

## Structs

Classes define types that support inheritance and polymorphism. They enable you to create sophisticated behaviors based on hierarchies of derived classes. By contrast, struct types are simpler types whose primary purpose is to store data values. Structs can't declare a base type; they implicitly derive from System.ValueType. You can't derive other struct types from a struct type. They're implicitly sealed.

```C#
//Copy
public struct Point
{
    public double X { get; }
    public double Y { get; }

    public Point(double x, double y) => (X, Y) = (x, y);
}
```

## Interfaces

An interface defines a contract that can be implemented by classes and structs. An interface can contain methods, properties, events, and indexers. An interface typically doesn't provide implementations of the members it defines—it merely specifies the members that must be supplied by classes or structs that implement the interface.

Interfaces may employ multiple inheritance. In the following example, the interface IComboBox inherits from both ITextBox and IListBox.

```C#
//Copy
interface IControl
{
    void Paint();
}

interface ITextBox : IControl
{
    void SetText(string text);
}

interface IListBox : IControl
{
    void SetItems(string[] items);
}

interface IComboBox : ITextBox, IListBox { }
```

Classes and structs can implement multiple interfaces. In the following example, the class EditBox implements both IControl and IDataBound.

```C#
//Copy
interface IDataBound
{
    void Bind(Binder b);
}

public class EditBox : IControl, IDataBound
{
    public void Paint() { }
    public void Bind(Binder b) { }
}
```

When a class or struct implements a particular interface, instances of that class or struct can be implicitly converted to that interface type. For example

```C#
//Copy
EditBox editBox = new EditBox();
IControl control = editBox;
IDataBound dataBound = editBox;
```

## Enums

An Enum type defines a set of constant values. The following enum declares constants that define different root vegetables:

```C#
//Copy
public enum SomeRootVegetables
{
    HorseRadish,
    Radish,
    Turnip
}
```

You can also define an enum to be used in combination as flags. The following declaration declares a set of flags for the four seasons. Any combination of the seasons may be applied, including an All value that includes all seasons:

```C#
//Copy
[Flags]
public enum Seasons
{
    None = 0,
    Summer = 1,
    Autumn = 2,
    Winter = 4,
    Spring = 8,
    All = Summer | Autumn | Winter | Spring
}
```

The following example shows declarations of both the preceding enums:

```C#
//Copy
var turnip = SomeRootVegetables.Turnip;

var spring = Seasons.Spring;
var startingOnEquinox = Seasons.Spring | Seasons.Autumn;
var theYear = Seasons.All;

```

## Nullable types

Variables of any type may be declared as non-nullable or nullable. A nullable variable can hold an additional null value, indicating no value. Nullable Value types (structs or enums) are represented by System.Nullable<T>. Non-nullable and Nullable Reference types are both represented by the underlying reference type. The distinction is represented by metadata read by the compiler and some libraries. The compiler provides warnings when nullable references are dereferenced without first checking their value against null. The compiler also provides warnings when non-nullable references are assigned a value that may be null. The following example declares a nullable int, initializing it to null. Then, it sets the value to 5. It demonstrates the same concept with a nullable string. For more information, see nullable value types and nullable reference types.

```C#
//Copy
int? optionalInt = default;
optionalInt = 5;
string? optionalText = default;
optionalText = "Hello World.";

```

## Tuples

C# supports tuples, which provides concise syntax to group multiple data elements in a lightweight data structure. You instantiate a tuple by declaring the types and names of the members between ( and ), as shown in the following example:

```C#
//Copy
(double Sum, int Count) t2 = (4.5, 3);
Console.WriteLine($"Sum of {t2.Count} elements is {t2.Sum}.");
// Output:
// Sum of 3 elements is 4.5.

```

Tuples provide an alternative for data structure with multiple members, without using the building blocks described in the next article.

# Program building blocks

The types described in the previous article are built using these building blocks: members, expressions, and statements.

Members
The members of a class are either static members or instance members. Static members belong to classes, and instance members belong to objects (instances of classes).

The following list provides an overview of the kinds of members a class can contain.

Constants: Constant values associated with the class
Fields: Variables that are associated of the class
Methods: Actions that can be performed by the class
Properties: Actions associated with reading and writing named properties of the class
Indexers: Actions associated with indexing instances of the class like an array
Events: Notifications that can be generated by the class
Operators: Conversions and expression operators supported by the class
Constructors: Actions required to initialize instances of the class or the class itself
Finalizers: Actions performed before instances of the class are permanently discarded
Types: Nested types declared by the class
Accessibility
Each member of a class has an associated accessibility, which controls the regions of program text that can access the member. There are six possible forms of accessibility. The access modifiers are summarized below.

public: Access isn't limited.
private: Access is limited to this class.
protected: Access is limited to this class or classes derived from this class.
internal: Access is limited to the current assembly (.exe or .dll).
protected internal: Access is limited to this class, classes derived from this class, or classes within the same assembly.
private protected: Access is limited to this class or classes derived from this type within the same assembly.
Fields
A field is a variable that is associated with a class or with an instance of a class.

A field declared with the static modifier defines a static field. A static field identifies exactly one storage location. No matter how many instances of a class are created, there's only ever one copy of a static field.

A field declared without the static modifier defines an instance field. Every instance of a class contains a separate copy of all the instance fields of that class.

In the following example, each instance of the Color class has a separate copy of the r, g, and b instance fields, but there's only one copy of the Black, White, Red, Green, and Blue static fields:

```C#
//Copy
public class Color
{
    public static readonly Color Black = new Color(0, 0, 0);
    public static readonly Color White = new Color(255, 255, 255);
    public static readonly Color Red = new Color(255, 0, 0);
    public static readonly Color Green = new Color(0, 255, 0);
    public static readonly Color Blue = new Color(0, 0, 255);

    public byte R { get; }
    public byte G { get; }
    public byte B { get; }

    public Color(byte r, byte g, byte b)
    {
        R = r;
        G = g;
        B = b;
    }
}
```

As shown in the previous example, read-only fields may be declared with a readonly modifier. Assignment to a read-only field can only occur as part of the field’s declaration or in a constructor in the same class.

## Methods

A method is a member that implements a computation or action that can be performed by an object or class. Static methods are accessed through the class. Instance methods are accessed through instances of the class.

Methods may have a list of parameters, which represent values or variable references passed to the method. Methods have a return type, which specifies the type of the value computed and returned by the method. A method’s return type is void if it doesn't return a value.

Like types, methods may also have a set of type parameters, for which type arguments must be specified when the method is called. Unlike types, the type arguments can often be inferred from the arguments of a method call and need not be explicitly given.

The signature of a method must be unique in the class in which the method is declared. The signature of a method consists of the name of the method, the number of type parameters, and the number, modifiers, and types of its parameters. The signature of a method doesn't include the return type.

When a method body is a single expression, the method can be defined using a compact expression format, as shown in the following example:

```C#
//Copy
public override ToString() => "This is an object";
```

## Parameters

Parameters are used to pass values or variable references to methods. The parameters of a method get their actual values from the arguments that are specified when the method is invoked. There are four kinds of parameters: value parameters, reference parameters, output parameters, and parameter arrays.

A value parameter is used for passing input arguments. A value parameter corresponds to a local variable that gets its initial value from the argument that was passed for the parameter. Modifications to a value parameter don't affect the argument that was passed for the parameter.

Value parameters can be optional, by specifying a default value so that corresponding arguments can be omitted.

A reference parameter is used for passing arguments by reference. The argument passed for a reference parameter must be a variable with a definite value. During execution of the method, the reference parameter represents the same storage location as the argument variable. A reference parameter is declared with the ref modifier. The following example shows the use of ref parameters.

```C#
//Copy
static void Swap(ref int x, ref int y)
{
    int temp = x;
    x = y;
    y = temp;
}

public static void SwapExample()
{
    int i = 1, j = 2;
    Swap(ref i, ref j);
    Console.WriteLine($"{i} {j}");    // "2 1"
}
```

An output parameter is used for passing arguments by reference. It's similar to a reference parameter, except that it doesn't require that you explicitly assign a value to the caller-provided argument. An output parameter is declared with the out modifier. The following example shows the use of out parameters using the syntax introduced in C# 7.

```C#
//Copy
static void Divide(int x, int y, out int result, out int remainder)
{
    result = x / y;
    remainder = x % y;
}

public static void OutUsage()
{
    Divide(10, 3, out int res, out int rem);
    Console.WriteLine($"{res} {rem}");	// "3 1"
}

```

A parameter array permits a variable number of arguments to be passed to a method. A parameter array is declared with the params modifier. Only the last parameter of a method can be a parameter array, and the type of a parameter array must be a single-dimensional array type. The Write and WriteLine methods of the System.Console class are good examples of parameter array usage. They're declared as follows.

```C#
//Copy
public class Console
{
    public static void Write(string fmt, params object[] args) { }
    public static void WriteLine(string fmt, params object[] args) { }
    // ...
}

```

Within a method that uses a parameter array, the parameter array behaves exactly like a regular parameter of an array type. However, in an invocation of a method with a parameter array, it's possible to pass either a single argument of the parameter array type or any number of arguments of the element type of the parameter array. In the latter case, an array instance is automatically created and initialized with the given arguments. This example

```C#
//Copy
int x, y, z;
x = 3;
y = 4;
z = 5;
Console.WriteLine("x={0} y={1} z={2}", x, y, z);
```

is equivalent to writing the following.

```C#
//Copy
int x = 3, y = 4, z = 5;

string s = "x={0} y={1} z={2}";
object[] args = new object[3];
args[0] = x;
args[1] = y;
args[2] = z;
Console.WriteLine(s, args);

```

# Method body and local variables

A method’s body specifies the statements to execute when the method is invoked.

A method body can declare variables that are specific to the invocation of the method. Such variables are called local variables. A local variable declaration specifies a type name, a variable name, and possibly an initial value. The following example declares a local variable i with an initial value of zero and a local variable j with no initial value.

```C#
//Copy
class Squares
{
    public static void WriteSquares()
    {
        int i = 0;
        int j;
        while (i < 10)
        {
            j = i * i;
            Console.WriteLine($"{i} x {i} = {j}");
            i = i + 1;
        }
    }
}
```

C# requires a local variable to be definitely assigned before its value can be obtained. For example, if the declaration of the previous i didn't include an initial value, the compiler would report an error for the later usages of i because i wouldn't be definitely assigned at those points in the program.

A method can use return statements to return control to its caller. In a method returning void, return statements can't specify an expression. In a method returning non-void, return statements must include an expression that computes the return value.

## Static and instance methods

A method declared with a static modifier is a static method. A static method doesn't operate on a specific instance and can only directly access static members.

A method declared without a static modifier is an instance method. An instance method operates on a specific instance and can access both static and instance members. The instance on which an instance method was invoked can be explicitly accessed as this. It's an error to refer to this in a static method.

The following Entity class has both static and instance members.

```C#
//Copy
class Entity
{
    static int s_nextSerialNo;
    int _serialNo;

    public Entity()
    {
        _serialNo = s_nextSerialNo++;
    }

    public int GetSerialNo()
    {
        return _serialNo;
    }

    public static int GetNextSerialNo()
    {
        return s_nextSerialNo;
    }

    public static void SetNextSerialNo(int value)
    {
        s_nextSerialNo = value;
    }
}
```

Each Entity instance contains a serial number (and presumably some other information that isn't shown here). The Entity constructor (which is like an instance method) initializes the new instance with the next available serial number. Because the constructor is an instance member, it's permitted to access both the \_serialNo instance field and the s_nextSerialNo static field.

The GetNextSerialNo and SetNextSerialNo static methods can access the s_nextSerialNo static field, but it would be an error for them to directly access the \_serialNo instance field.

The following example shows the use of the Entity class.

```C#
//Copy
Entity.SetNextSerialNo(1000);
Entity e1 = new Entity();
Entity e2 = new Entity();
Console.WriteLine(e1.GetSerialNo());          // Outputs "1000"
Console.WriteLine(e2.GetSerialNo());          // Outputs "1001"
Console.WriteLine(Entity.GetNextSerialNo());  // Outputs "1002"
```

The `SetNextSerialNo` and `GetNextSerialNo` static methods are invoked on the class whereas the GetSerialNo instance method is invoked on instances of the class.

## Virtual, override, and abstract methods

When an instance method declaration includes a `virtual` modifier, the method is said to be a virtual method. When no virtual modifier is present, the method is said to be a _nonvirtual method_.

When a virtual method is invoked, the run-time type of the instance for which that invocation takes place determines the actual method implementation to invoke. In a nonvirtual method invocation, the _compile-time_ type of the instance is the determining factor.

A virtual method can be _overridden_ in a derived class. When an instance method declaration includes an override modifier, the method overrides an inherited virtual method with the same signature. A virtual method declaration introduces a new method. An override method declaration specializes an existing inherited virtual method by providing a new implementation of that method.

An _abstract_ method is a virtual method with no implementation. An abstract method is declared with the abstract modifier and is permitted only in an abstract class. An abstract method must be overridden in every non-abstract derived class.

The following example declares an abstract class, `Expression`, which represents an expression tree node, and three derived classes, `Constant`, `VariableReference`, and `Operation`, which implement expression tree nodes for constants, variable references, and arithmetic operations. (This example is similar to, but not related to the expression tree types).

````C#
//Copy
public abstract class Expression
{
    public abstract double Evaluate(Dictionary<string, object> vars);
}

public class Constant : Expression
{
    double _value;

    public Constant(double value)
    {
        _value = value;
    }

    public override double Evaluate(Dictionary<string, object> vars)
    {
        return _value;
    }
}

public class VariableReference : Expression
{
    string _name;

    public VariableReference(string name)
    {
        _name = name;
    }

    public override double Evaluate(Dictionary<string, object> vars)
    {
        object value = vars[_name] ?? throw new Exception($"Unknown variable: {_name}");
        return Convert.ToDouble(value);
    }
}

public class Operation : Expression
{
    Expression _left;
    char _op;
    Expression _right;

    public Operation(Expression left, char op, Expression right)
    {
        _left = left;
        _op = op;
        _right = right;
    }

    public override double Evaluate(Dictionary<string, object> vars)
    {
        double x = _left.Evaluate(vars);
        double y = _right.Evaluate(vars);
        switch (_op)
        {
            case '+': return x + y;
            case '-': return x - y;
            case '*': return x * y;
            case '/': return x / y;

            default: throw new Exception("Unknown operator");
        }
    }
}
The previous four classes can be used to model arithmetic expressions. For example, using instances of these classes, the _expression_ `x + 3` can be represented as follows.

```C#
//Copy
Expression e = new Operation(
    new VariableReference("x"),
    '+',
    new Constant(3));
````

The `Evaluate` method of an `Expression` instance is invoked to evaluate the given expression and produce a double value. The method takes a `Dictionary` argument that contains variable names (as keys of the entries) and values (as values of the entries). Because `Evaluate` is an abstract method, non-abstract classes derived from `Expression` must override `Evaluate`.

A Constant's implementation of `Evaluate` simply returns the stored constant. A `VariableReference`'s implementation looks up the variable name in the dictionary and returns the resulting value. An Operation's implementation first evaluates the left and right operands (by recursively invoking their `Evaluate` methods) and then performs the given arithmetic operation.

The following program uses the `Expression` classes to evaluate the expression `x * (y + 2)` for different values of `x` and `y`.

```C#
//Copy
Expression e = new Operation(
    new VariableReference("x"),
    '*',
    new Operation(
        new VariableReference("y"),
        '+',
        new Constant(2)
    )
);


Dictionary<string, object> vars = new Dictionary<string, object>();
vars["x"] = 3;
vars["y"] = 5;
Console.WriteLine(e.Evaluate(vars)); // "21"
vars["x"] = 1.5;
vars["y"] = 9;
Console.WriteLine(e.Evaluate(vars)); // "16.5"
```

## Method overloading

Method _overloading_ permits multiple methods in the same class to have the same name as long as they have unique signatures. When compiling an invocation of an overloaded method, the compiler uses _overload resolution_ to determine the specific method to invoke. Overload resolution finds the one method that best matches the arguments. If no single best match can be found, an error is reported. The following example shows overload resolution in effect. The comment for each invocation in the `UsageExample` method shows which method is invoked.

```C#
//Copy
class OverloadingExample
{
    static void F() => Console.WriteLine("F()");
    static void F(object x) => Console.WriteLine("F(object)");
    static void F(int x) => Console.WriteLine("F(int)");
    static void F(double x) => Console.WriteLine("F(double)");
    static void F<T>(T x) => Console.WriteLine("F<T>(T)");
    static void F(double x, double y) => Console.WriteLine("F(double, double)");

    public static void UsageExample()
    {
        F();            // Invokes F()
        F(1);           // Invokes F(int)
        F(1.0);         // Invokes F(double)
        F("abc");       // Invokes F<string>(string)
        F((double)1);   // Invokes F(double)
        F((object)1);   // Invokes F(object)
        F<int>(1);      // Invokes F<int>(int)
        F(1, 1);        // Invokes F(double, double)
    }
```

As shown by the example, a particular method can always be selected by explicitly casting the arguments to the exact parameter types and type arguments.

## Other function members

Members that contain executable code are collectively known as the function members of a class. The preceding section describes methods, which are the primary types of function members. This section describes the other kinds of function members supported by C#: constructors, properties, indexers, events, operators, and finalizers.

The following example shows a generic class called `MyList<T>`, which implements a growable list of objects. The class contains several examples of the most common kinds of function members.

```C#
//Copy
public class MyList<T>
{
    const int DefaultCapacity = 4;

    T[] _items;
    int _count;

    public MyList(int capacity = DefaultCapacity)
    {
        _items = new T[capacity];
    }

    public int Count => _count;

    public int Capacity
    {
        get =>  _items.Length;
        set
        {
            if (value < _count) value = _count;
            if (value != _items.Length)
            {
                T[] newItems = new T[value];
                Array.Copy(_items, 0, newItems, 0, _count);
                _items = newItems;
            }
        }
    }

    public T this[int index]
    {
        get => _items[index];
        set
        {
            _items[index] = value;
            OnChanged();
        }
    }

    public void Add(T item)
    {
        if (_count == Capacity) Capacity = _count * 2;
        _items[_count] = item;
        _count++;
        OnChanged();
    }
    protected virtual void OnChanged() =>
        Changed?.Invoke(this, EventArgs.Empty);

    public override bool Equals(object other) =>
        Equals(this, other as MyList<T>);

    static bool Equals(MyList<T> a, MyList<T> b)
    {
        if (Object.ReferenceEquals(a, null)) return Object.ReferenceEquals(b, null);
        if (Object.ReferenceEquals(b, null) || a._count != b._count)
            return false;
        for (int i = 0; i < a._count; i++)
        {
            if (!object.Equals(a._items[i], b._items[i]))
            {
                return false;
            }
        }
        return true;
    }

    public event EventHandler Changed;

    public static bool operator ==(MyList<T> a, MyList<T> b) =>
        Equals(a, b);

    public static bool operator !=(MyList<T> a, MyList<T> b) =>
        !Equals(a, b);
}
```

## Constructors

C# supports both instance and static constructors. An instance constructor is a member that implements the actions required to initialize an instance of a class. A static constructor is a member that implements the actions required to initialize a class itself when it's first loaded.

A constructor is declared like a method with no return type and the same name as the containing class. If a constructor declaration includes a `static` modifier, it declares a static constructor. Otherwise, it declares an instance constructor.

Instance constructors can be overloaded and can have optional parameters. For example, the `MyList<T>` class declares one instance constructor with a single optional int parameter. Instance constructors are invoked using the new operator. The following statements allocate two `MyList<string>` instances using the constructor of the MyList class with and without the optional argument.

```C#
//Copy
MyList<string> list1 = new MyList<string>();
MyList<string> list2 = new MyList<string>(10);
```

Unlike other members, instance constructors aren't inherited. A class has no instance constructors other than those constructors actually declared in the class. If no instance constructor is supplied for a class, then an empty one with no parameters is automatically provided.

## Properties

_Properties_ are a natural extension of fields. Both are named members with associated types, and the syntax for accessing fields and properties is the same. However, unlike fields, properties don't denote storage locations. Instead, properties have accessors that specify the statements executed when their values are read or written.

A property is declared like a field, except that the declaration ends with a get accessor or a set accessor written between the delimiters { and } instead of ending in a semicolon. A property that has both a get accessor and a set accessor is a read-write property, a property that has only a get accessor is a read-only property, and a property that has only a set accessor is a _write-only_ property.

A get accessor corresponds to a parameterless method with a return value of the property type. A set accessor corresponds to a method with a single parameter named value and no return type. The get accessor computes the value of the property. The set accessor provides a new value for the property. When the property is the target of an assignment, or the operand of `++` or `--`, the set accessor is invoked. In other cases where the property is referenced, the get accessor is invoked.

The `MyList<T>` class declares two properties, Count and Capacity, which are read-only and read-write, respectively. The following code is an example of use of these properties:

```C#
//Copy
MyList<string> names = new MyList<string>();
names.Capacity = 100;   // Invokes set accessor
int i = names.Count;    // Invokes get accessor
int j = names.Capacity; // Invokes get accessor
```

Similar to fields and methods, C# supports both instance properties and static properties. Static properties are declared with the static modifier, and instance properties are declared without it.

The accessor(s) of a property can be virtual. When a property declaration includes a `virtual`, `abstract`, or `override` modifier, it applies to the accessor(s) of the property.

## Indexers

An indexer is a member that enables objects to be indexed in the same way as an array. An indexer is declared like a property except that the name of the member is this followed by a parameter list written between the delimiters `[` and `]`. The parameters are available in the accessor(s) of the indexer. Similar to properties, indexers can be read-write, read-only, and write-only, and the accessor(s) of an indexer can be virtual.

The `MyList<T>` class declares a single read-write indexer that takes an int parameter. The indexer makes it possible to index `MyList<T>` instances with int values. For example:

```C#
//Copy
MyList<string> names = new MyList<string>();
names.Add("Liz");
names.Add("Martha");
names.Add("Beth");
for (int i = 0; i < names.Count; i++)
{
    string s = names[i];
    names[i] = s.ToUpper();
}
```

Indexers can be overloaded. A class can declare multiple indexers as long as the number or types of their parameters differ.

## Events

An _event_ is a member that enables a class or object to provide notifications. An event is declared like a field except that the declaration includes an `event` keyword and the type must be a delegate type.

Within a class that declares an event member, the event behaves just like a field of a delegate type (provided the event isn't abstract and doesn't declare accessors). The field stores a reference to a delegate that represents the event handlers that have been added to the event. If no event handlers are present, the field is null.

The `MyList<T>` class declares a single event member called `Changed`, which indicates that a new item has been added to the list. The Changed event is raised by the `OnChanged` virtual method, which first checks whether the event is `null` (meaning that no handlers are present). The notion of raising an event is precisely equivalent to invoking the delegate represented by the event. There are no special language constructs for raising events.

Clients react to events through event handlers. Event handlers are attached using the `+=` operator and removed using the `-=` operator. The following example attaches an event handler to the `Changed` event of a `MyList<string>`.

```C#
//Copy
class EventExample
{
    static int s_changeCount;

    static void ListChanged(object sender, EventArgs e)
    {
        s_changeCount++;
    }

    public static void Usage()
    {
        var names = new MyList<string>();
        names.Changed += new EventHandler(ListChanged);
        names.Add("Liz");
        names.Add("Martha");
        names.Add("Beth");
        Console.WriteLine(s_changeCount); // "3"
    }
}
```

For advanced scenarios where control of the underlying storage of an event is desired, an event declaration can explicitly provide add and remove accessors, which are similar to the set accessor of a property.

# Operators

An _operator_ is a member that defines the meaning of applying a particular expression operator to instances of a class. Three kinds of operators can be defined: unary operators, binary operators, and conversion operators. All operators must be declared as `public` and `static`.

The `MyList<T>` class declares two operators, operator `==` and operator `!=`. These overridden operators give new meaning to expressions that apply those operators to MyList instances. Specifically, the operators define equality of two `MyList<T>` instances as comparing each of the contained objects using their Equals methods. The following example uses the `==` operator to compare two `MyList<int>` instances.

```C#
//Copy
MyList<int> a = new MyList<int>();
a.Add(1);
a.Add(2);
MyList<int> b = new MyList<int>();
b.Add(1);
b.Add(2);
Console.WriteLine(a == b);  // Outputs "True"
b.Add(3);
Console.WriteLine(a == b);  // Outputs "False"
```

The first `Console.WriteLine` outputs True because the two lists contain the same number of objects with the same values in the same order. Had `MyList<T>` not defined `operator ==`, the first `Console.WriteLine` would have output `False` because `a` and `b` reference different `MyList<int>` instances.

## Finalizers

A _finalizer_ is a member that implements the actions required to finalize an instance of a class. Typically, a finalizer is needed to release unmanaged resources. Finalizers can't have parameters, they can't have accessibility modifiers, and they can't be invoked explicitly. The finalizer for an instance is invoked automatically during garbage collection. For more details, see the article on finalizers.

The garbage collector is allowed wide latitude in deciding when to collect objects and run finalizers. Specifically, the timing of finalizer invocations isn't deterministic, and finalizers may be executed on any thread. For these and other reasons, classes should implement finalizers only when no other solutions are feasible.

The using statement provides a better approach to object destruction.

## Expressions

Expressions are constructed from operands and operators. The operators of an expression indicate which operations to apply to the operands. Examples of operators include +, -, \*, /, and new. Examples of operands include literals, fields, local variables, and expressions.

When an expression contains multiple operators, the precedence of the operators controls the order in which the individual operators are evaluated. For example, the expression x + y _ z is evaluated as x + (y _ z) because the \* operator has higher precedence than the + operator.

When an operand occurs between two operators with the same precedence, the associativity of the operators controls the order in which the operations are performed:

- Except for the assignment and null-coalescing operators, all binary operators are left-associative, meaning that operations are performed from left to right. For example, `x + y + z` is evaluated as `(x + y) + z`.
- The assignment operators, the null-coalescing `??` and `??=` operators, and the conditional operator `?:` are right-associative, meaning that operations are performed from right to left. For example, `x = y = z` is evaluated as `x = (y = z)`.

Precedence and associativity can be controlled using parentheses. For example, `x + y * z` first multiplies `y` by `z` and then adds the result to `x`, but `(x + y) * z` first adds `x` and `y` and then multiplies the result by z.

Most operators can be [overloaded](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/operator-overloading). Operator overloading permits user-defined operator implementations to be specified for operations where one or both of the operands are of a `user-defined class` or `struct` type.

C# provides a number of operators to perform arithmetic, logical, bitwise and shift operations and equality and order comparisons.

For the complete list of C# operators ordered by precedence level, see C# operators.

## Statements

The actions of a program are expressed using statements. C# supports several different kinds of statements, a number of which are defined in terms of embedded statements.

- A _block_ permits multiple statements to be written in contexts where a single statement is allowed. A block consists of a list of statements written between the delimiters `{` and `}`.
- _Declaration_ statements are used to declare local variables and constants.
- _Expression_ statements are used to evaluate expressions. Expressions that can be used as statements include method invocations, object allocations using the new operator, assignments using `=` and the compound assignment operators, increment and decrement operations using the `++` and `--` operators and await expressions.
- _Selection statements_ are used to select one of a number of possible statements for execution based on the value of some expression. This group contains the `if` and `switch` statements.
- _Iteration_ statements are used to execute repeatedly an embedded statement. This group contains the `while`, `do`, `for`, and `foreach` statements.
  Jump statements are used to transfer control. This group contains the `break`, `continue`, `goto`, `throw`, `return`, and `yield` statements.
- The _try...catch_ statement is used to catch exceptions that occur during execution of a block, and the try...`finally` statement is used to specify finalization code that is always executed, whether an exception occurred or not.
- The `checked` and `unchecked` statements are used to control the overflow-checking context for integral-type arithmetic operations and conversions.
- The `lock` statement is used to obtain the mutual-exclusion lock for a given object, execute a statement, and then release the lock.
- The `using` statement is used to obtain a resource, execute a statement, and then dispose of that resource.

The following lists the kinds of statements that can be used:

- Local variable declaration.
- Local constant declaration.
- Expression statement.
- if statement.
- switch statement.
- while statement.
- do statement.
- for statement.
- foreach statement.
- break statement.
- continue statement.
- goto statement.
- return statement.
- yield statement.
- throw statements and try statements.
- checked and unchecked statements.
- lock statement.
- using statement.

[Introduction to C# Tutorials](https://docs.microsoft.com/en-us/dotnet/csharp/tutorials/intro-to-csharp/)

```

```