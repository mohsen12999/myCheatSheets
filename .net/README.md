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

* TDD: Test Driven Development (aka Test Driven Design)
* [Modern Dev Practices Unit Testing high](https://www.youtube.com/watch?v=4averylLdjQ&t=276s)
  * xunit
  * xunit.runner.visualstudio
  * moq
* [xunit](https://xunit.net/)
* MSpec Visual Studio Test Adapter [Machine.VSTestAdapter](https://marketplace.visualstudio.com/items?itemName=JonathanWilkins.MachineVSTestAdapter)
