# BetaSoftwares.Fixture

## **Installation**
To install **BetaSoftwares.Fixture**, you can either browse the Package Manager or run the following command in the <a href='#https://docs.microsoft.com/fr-fr/nuget/tools/package-manager-console'>Package Manager Console</a> :

```
PM> Install-Package BetaSoftwares.Fixture
```

<hr>

## **Usage**
<br>
To start using **BetaSoftwares.Fixture,** you will first need to create an instance of the Fixture class :

```cs
using BetaSoftwares.Fixtures

Fixture fixture = new Fixture();
```

 ### **Create**
 To generate a new fixture of any type, use the **Fixture.Create** method :

 ```cs
 string random = fixture.Create<string>();
// or..
 string random = fixture.Create(typeof(string));
 ```

### **CreateMany**
To generate many fixtures at the same time, you can use the **Fixture.CreateMany** method :

```cs
ICollection random = fixture.CreateMany<string>();
// or..
ICollection random = fixture.CreateMany(typeof(string));
```

### **AddManyTo**
To add many fixtures an already existing list, you can use the **Fixture.AddManyTo** method :

```cs
List<string> list = new List<string>();
// Add 5 fixture to the list
fixture.AddManyTo(list, 5);
int count = list.Count; // count = 5
```

### **Build**,  **With**, **Without** and **Do**
You can also customize a fixture on creation using the **Fixture.Build** with the **FixtureDefinition.With**,  **FixtureDefinition.Without** and **FixtureDefinition.Do** methods :

```cs
// With
ICollection random = fixture.Build<MyClass>().With(c => c.MyString, "Hello world").Create();
// Without
ICollection random = fixture.Build<MyClass>().Without(c => c.MyString).Create();
// Do
ICollection random = fixture.Build<MyClass>().Do(c => c.MyList.Clear()).Create();
// You can mix .With, .Without and .Do
ICollection random = fixture.Build<MyClass>().With(c => c.MyString, "Hello world").Do(c => c.MyList.Clear()).Create();
```

### **Register**
To register a type default value, you can use the **Fixture.Register** method :

```cs
// Registers a new default value
fixture.Register<IMyInterface>(() => new MyClass());
// The instance will be of the registered type
MyClass myClass = fixture.Create<IMyInterface>();
```

### **Customize**
To customize a complex type default properties, you can use the **Fixture.Customize** method :

```cs
// Customize the class default properties
_fixture.Customize<ComplexType>(c => c.With(c => c.MyInteger, 42));
// The instance will have the custom properties
ComplexType myClass = fixture.Create<ComplexType>();
int value = myClass.MyInteger; // value = 42
```

## Supported types
Here is the index of currently supported types. If the type is not supported, the property will be set to the default value of the type.

### Basic types :
- [string](https://msdn.microsoft.com/en-us/library/system.string)
- [bool](https://msdn.microsoft.com/en-us/library/system.boolean)
- [object](https://msdn.microsoft.com/en-us/library/system.object)
- [char](https://msdn.microsoft.com/en-us/library/system.char)
- [short](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/short)
- [ushort](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/ushort)
- [int](https://msdn.microsoft.com/fr-fr/library/system.int32(v=vs.110).aspx)
- [uint](https://msdn.microsoft.com/en-us/library/system.uint32(v=vs.110).aspx)
- [float](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/float)
- [double](https://msdn.microsoft.com/en-us/library/system.double(v=vs.110).aspx)
- [decimal](https://msdn.microsoft.com/en-us/library/system.decimal(v=vs.110).aspx)
- [long](https://msdn.microsoft.com/en-us/library/system.int64(v=vs.110).aspx)
- [ulong](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/ulong)
- [byte](https://msdn.microsoft.com/fr-fr/library/system.byte(v=vs.110).aspx)
- [sbyte](https://msdn.microsoft.com/en-us/library/system.sbyte(v=vs.110).aspx)

### Data structures :
- [ICollection](https://msdn.microsoft.com/en-us/library/92t2ye13(v=vs.110).aspx)
- [IDictionary](https://msdn.microsoft.com/fr-fr/library/s4ys34ea(v=vs.110).aspx)
- [Tuple](https://msdn.microsoft.com/fr-fr/library/system.tuple(v=vs.110).aspx)
