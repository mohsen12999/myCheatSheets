# .Net

## .net cli

## Redis

- package:
  - Microsoft.Extentions.Caching.Abstractions
  - Microsoft.Extentions.Caching.redis
- startup -> configureServices `services.addDistributedRedisCache(option => { option.configuration = "aspnetcore.redis.cache.windows.net:3680,passwors=1212" })`
- in controller

  - `private AlphaCacheServices _alphaCache`
  - value in constroctor (inject)
  - use: `var result = await _alphaCache.GetEntry("a")`
  - use: `var result = await _alphaCache.GetAsync("a");`
    `var p = json.deserializeObject<person>(unicode.utf8.getstring(entry))`
  - save: `await _alphaCache.SetSync()`

- Stackexchange redis package

## Test

- TDD: Test Driven Development (aka Test Driven Design) -> [Test Driven Development](https://deviq.com/test-driven-development/)
- [Modern Dev Practices Unit Testing high](https://www.youtube.com/watch?v=4averylLdjQ&t=276s)
  - xunit
  - xunit.runner.visualstudio
  - moq
- [xunit](https://xunit.net/)
- MSpec Visual Studio Test Adapter [Machine.VSTestAdapter](https://marketplace.visualstudio.com/items?itemName=JonathanWilkins.MachineVSTestAdapter)

- [Unit testing best practices with .NET Core and .NET Standard](https://docs.microsoft.com/en-us/dotnet/core/testing/unit-testing-best-practices)

- [Integration tests in ASP.NET Core](https://docs.microsoft.com/en-us/visualstudio/test/live-unit-testing-start?view=vs-2019)

### unit test

- Characteristics: `Fast`, `Isolated`, `Repeatable`, `Self-Checking`, `Timely`

* xUnit
* NUnit
* MSTest

- Best practices
  - Naming your tests -> 3 part -> Add_SingleNumber_ReturnsSameNumber
    - `name` of the method being tested
    - `scenario` under which it's being tested.
    - `expected` behavior when the scenario is invoked
  - Arranging your tests -> Arrange, Act, Assert
    - Arrange your objects, creating and setting them up as necessary.
    - Act on an object.
    - Assert that something is as expected.
  - Write minimally passing tests -> the simplest possible
  - Avoid magic strings -> naming to describe value
  - Avoid logic in tests -> `if`, `while`, `for`, `switch`, ...
  - Avoid multiple asserts -> for one thing
  - Validate private methods by unit testing public methods
  - Stub static references -> must have full control of the system under test

#### xUnit

```cs
[Fact]
public void IsPrime_InputIs1_ReturnFalse()
{
    var result = _primeService.IsPrime(1);

    Assert.False(result, "1 should not be prime");
    // Assert.Equal(0, actual);
}
```

```cs
[Theory]
[InlineData(-1)]
[InlineData(0)]
[InlineData(1)]
// [InlineData("1,2,3", 6)]
public void IsPrime_ValuesLessThan2_ReturnFalse(int value)
{
    var result = _primeService.IsPrime(value);

    Assert.False(result, $"{value} should not be prime");
}
```

#### nUnit

```cs
[Test]
public void IsPrime_InputIs1_ReturnFalse()
{
    PrimeService primeService = CreatePrimeService();
    var result = primeService.IsPrime(1);

    Assert.IsFalse(result, "1 should not be prime");
}
```

```cs
[TestCase(-1)]
[TestCase(0)]
[TestCase(1)]
public void IsPrime_ValuesLessThan2_ReturnFalse(int value)
{
    var result = _primeService.IsPrime(value);

    Assert.IsFalse(result, $"{value} should not be prime");
}
```

```
[Test]
[ExpectedException(typeof(ArgumentException))]
public void ShouldGetAnArgumentException()
{
    // expect for Exception to success testing
}
```

* SetUp, TestFixtureSetUp‌ -> make construct method for test class

#### MSTest

```cs
[TestClass]
public class PrimeService_IsPrimeShould
{
    private readonly PrimeService _primeService;

    public PrimeService_IsPrimeShould()
    {
        _primeService = new PrimeService();
    }

    [TestMethod]
    public void IsPrime_InputIs1_ReturnFalse()
    {
        var result = _primeService.IsPrime(1);

        Assert.IsFalse(result, "1 should not be prime");
    }
}
```

```cs
[DataTestMethod]
[DataRow(-1)]
[DataRow(0)]
[DataRow(1)]
public void IsPrime_ValuesLessThan2_ReturnFalse(int value)
{
    var result = _primeService.IsPrime(value);

    Assert.IsFalse(result, $"{value} should not be prime");
}
```

### Integration tests

- [Integration tests in ASP.NET Core](https://docs.microsoft.com/en-us/aspnet/core/test/integration-tests?view=aspnetcore-3.1#test-app-prerequisites)
- System Under Test -> `SUT`
- class under test or code under test -> `CUT`

## to see

- tdd net core
  [Creating Web API in ASP.NET Core 2.0](https://www.codingame.com/playgrounds/35462/creating-web-api-in-asp-net-core-2-0/part-3---integration-tests)
  [Build a TDD Restful WebAPI for a Blog using dotnet core](https://dev.to/adegokesimi/build-a-tdd-restful-webapi-for-a-blog-using-dotnet-core-5fo8)
  [Beginning Test-Driven Development in .NET Core](https://fullstackmark.com/post/8/beginning-test-driven-development-in-net-core)
  [elmah](https://elmah.ir)
  [30 Days of TDD: Day One – What is TDD and Why Should I Use It?](http://blogs.telerik.com/james-bender/posts.aspx/13-09-09/30-days-tdd-day-one-what-is-tdd)

## Solid

- Single Responsibility Principle
- Open/Close Principle -> open for extension, but closed for modification
- Liskov Substitution Principle -> Objects in a program should be replaceable with instances of their subtypes without altering the correctness of that program
- Interface Segregation Principle -> Many client-specific interfaces are better than one general-purpose interface
- Dependency Inversion Principle -> depend upon abstractions, [not] concretions

## DI Framewrok

- `DI Framewrok` -> Dependency Injection, like:
  - [Ninject](http://www.ninject.org/)
  - [Structure Map](http://ww1.structuremap.net/)
  - [Microsoft Unity](https://github.com/unitycontainer/unity)

- ninject main parts:
  - The Application - your program
  - The Kernel/Container - the interface for ninject
  - The Provider - the rules for creat class
  - The Created Class - Instance of class make by Kernel

- [ninject cheat sheet](https://lukewickstead.wordpress.com/2013/01/18/ninject-cheat-sheet/)

## Refactoring

TDD - `Red, Green, Refactor`
  - Red: faild - writing test
  - Green: pass - write code to pass test
  - Refactor: improve code better again and again

- readable, flexible, optimal ,...

