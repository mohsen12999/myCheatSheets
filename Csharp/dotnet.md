# .Net


## .net cli

## Problem

* solve problem with `scanf` in visual studio -> go to project properties -> Configuration Properties -> C/C++ -> General -> SDL checks -> No.

## Redis

* package:
  * Microsoft.Extentions.Caching.Abstractions
  * Microsoft.Extentions.Caching.redis
* startup -> configureServices `services.addDistributedRedisCache(option => { option.configuration = "aspnetcore.redis.cache.windows.net:3680,passwors=1212" })`
* in controller
  * `private AlphaCacheServices _alphaCache`
  * value in constroctor (inject)
  * use: `var result = await _alphaCache.GetEntry("a")`
  * use: `var result = await _alphaCache.GetAsync("a");`
        `var p = json.deserializeObject<person>(unicode.utf8.getstring(entry))`
  * save: `await _alphaCache.SetSync()`

* Stackexchange redis package

## Test

* [Unit testing best practices with .NET Core and .NET Standard](https://docs.microsoft.com/en-us/dotnet/core/testing/unit-testing-best-practices)

### xUnit

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

### nUnit

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

### MSTest

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


