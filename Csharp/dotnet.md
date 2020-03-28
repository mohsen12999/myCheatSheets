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

```cs
[Test]
[ExpectedException(typeof(ArgumentException))]
public void ShouldGetAnArgumentException()
{
    // expect for Exception to success testing
}
```

- SetUp, TestFixtureSetUp‌ -> make construct method for test class
- SetUp -> make new object for every test, TestFixtureSetUp‌ -> make one for all

```cs
private ClassName _className;

[SetUp]
public void SetupClassNameTests()
{
	_className = new ClassName()
}
```

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

- [Integration tests in ASP.NET Core](https://docs.microsoft.com/en-us/aspnet/core/test/integration-tests?view=aspnetcore-3.1)
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
- DRY - `Don’t Repeat Yourself`

## Mocking

- Fakes – is an object that has some sort of actual working mechanism inside that returns a predictable result, but doesn’t implement the actual production logic.
- Stubs – is an object that will return a specific result based on a specific set of input. If I tell my stub to return “John Doe” whenever I ask it for the person with ID number 42, than that’s what it will do. However when I ask a stub for a person with an ID number 41, it doesn’t know what to do.
- Mocks – is a much more sophisticated version of a Stub. It will still return values like a stub, but it can also be programmed with expectations in terms of how many times each method should be called, in which order and with what data. Mocks provide features that ensure that our code under test is using it’s dependencies in a very specific way.
- Spy – is type of mock that takes an object and instead of creating a new mock object replaces the methods that the tester wants to mock. Spies are great for testing legacy (non TDD code) but you must be very careful as missing something that should have been mocked can have disastrous results
- Dummy – is an object that can be passed as a replacement for another object, but is never used. Dummies are essentially placeholders.

- for do thats we have `Mocking Frameworks` such as `JustMock` or `JustMock` Lite

```cs
using Telerik.JustMock
// ...
var orderDataService = Mock.Create<iorderdataservice>(); // make for injection dependency for making object
Mock.Arrange(() => orderDataService.Save(Arg.IsAny<order>()))
	.Returns(expectedOrderId)
	.OccursOnce(); // only execute one time
OrderService orderService = new OrderService(orderDataService); // making object
// ...
Mock.Assert(orderDataService); //check rule for mock -> occure one time
```

- `OccursNever()` -> never reach some place in code
- `InOrder()` -> run in order we write here

## Defects

- defects are really just requirements that have yet to be discovered.
- “zombie” defect: a defect that has been “fixed” on several occasions but always seems to find a way to come back.

## Other Tests

- Integration Tests - is similar to unit testing but instead of running our code in isolation we make a point of using the other components, classes and external resources for our tests.
- User Interface Tests
- Performance and Stress Tests
- Security Tests
- User Acceptance Tests - at some point in time you need a human being to get their eyes on the application.

## Test Eventually Development

- TED is write their unit tests after they’ve written the code under test.

https://www.telerik.com/blogs/30-days-of-tdd-day-24-strictly-mocking

## ASP.NET Core integration tests

- Microsoft.AspNetCore.Mvc.Testing package
- Microsoft.NET.Sdk.Web sdk
