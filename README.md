# BetaSoftwares.Fixture

## **Installation**
To install **BetaSoftwares.Fixture**, you can either browse the Package Manager or run the following command in the <a href='#https://docs.microsoft.com/fr-fr/nuget/tools/package-manager-console'>Package Manager Console</a> :

```
PM> Install-Package BetaSoftwares.Fixture
```

<hr>

## **Usage**
<br>
To start using **BetaSoftwares.Fixture**, you will first need to create an instance of the Fixture class :

```cs
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

### **Build**,  **With** and **Do**
You can also customize a fixture on creation using the **Fixture.Build** with the  **FixtureDefinition.With** and **FixtureDefinition.Do** methods :

```cs
// Notice the .Create at the end
ICollection random = fixture.Build<MyClass>().With(c => c.MyString, "Hello world").Create();
// You can mix .With and .Do
ICollection random = fixture.Build<MyClass>().With(c => c.MyString, "Hello world").Do(c => c.MyList.Clear()).Create();
// You can chain .With and .Do as much as you want
ICollection random = fixture.Build<MyClass>().With(c => c.MyString, "Hello world").Do(c => c.MyList.Clear()).With(c => c.MyInteger, 42).Create();
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
