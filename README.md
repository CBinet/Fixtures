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
*(Example given with the string type)*

 ```cs
 // This works
 string random = fixture.Create<string>();
 // This also works
 string random = fixture.Create(typeof(string));
 ```

### **CreateMany**
To generate many fixture at the same time, you can use the **Fixture.CreateMany** method : *(Example given with the string type)*

```cs
// This works
ICollection random = fixture.CreateMany<string>();
// This also works
ICollection random = fixture.CreateMany(typeof(string));
// Note that this is the same as this
ICollection random = fixture.Create<List<string>>();
// Or this
ICollection random = fixture.Create(typeof(List<string>));
```

### **Build** and  **With** and **Do**
You can also customize a fixture on creation using the **Fixture.Build** with the  **FixtureDefinition.With** and **FixtureDefinition.Do** methods : *(Example given a basic MyClass type)*

```cs
// Notice the .Create at the end
ICollection random = fixture.Build<MyClass>().With(c => c.MyString, "Hello world").Create();
// You can mix .With and .Do
ICollection random = fixture.Build<MyClass>().With(c => c.MyString, "Hello world").Do(c => c.MyList.Clear()).Create();
// You can chain .With and .Do as much as you want
ICollection random = fixture.Build<MyClass>().With(c => c.MyString, "Hello world").Do(c => c.MyList.Clear()).With(c => c.MyInteger, 42).Create();
```
