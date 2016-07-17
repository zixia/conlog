# brolog  [![Build Status](https://travis-ci.org/zixia/brolog.svg?branch=master)](https://travis-ci.org/zixia/brolog)

Brolog is Logger for Angular in Browser like Npmlog.

[![npm version](https://badge.fury.io/js/brolog.svg)](https://badge.fury.io/js/brolog)

# Feature

1. Support import with TypeScript. (typing file [index.d.ts](https://github.com/zixia/brolog/blob/master/index.d.ts))
1. Support Angular2 & SystemJS. (demo project [git repository](https://github.com/zixia/brolog-angular-demo))
1. Support show **real** line number in browser console.
    > What I really get frustrated by is that I cannot wrap console.* and preserve line numbers

    [We enabled this in Chrome DevTools via blackboxing a bit ago.](https://gist.github.com/paulirish/c307a5a585ddbcc17242)
1. Certainly it can run under nodejs. (Just for test & fun. example [here](https://github.com/zixia/brolog/blob/master/example/npm-like-logger.js))

# Example

Here's two example: 

1. the first one is demo for easy to use in browser, and how it looks like npmlog.
1. the second one is demo for intergrate with angular DI & systemjs.

## 1. Dead easy for use in Browser

You can enable Brolog in your page by simple add a `<script src="">` tag.

```
<html>
  <head>
    <script src="//zixia.github.io/brolog/src/brolog.js"></script>
  </head>
  <body>
    <h1>Brolog in Browser Demo</h1>
    <script>

      var log = Brolog('VERBOSE')

      log.info('Test', '123 info message')
      log.verbose('Test', '123 verbose message')
      log.silly('Test', '123 silly message')

    </script>
  </body>
</html>
```

Link: [Live demo on Plunker](http://embed.plnkr.co/tvO9MHscHuOM5XvZRIU6/)

## 2. Setup for use in Angular

`Brolog` is writen mainly for act as a logger with Angular. Here's how to Inject Brolog in Angular.

1. install brolog  
  ```
  $ npm install brolog --save
  ```
  
1. setup SystemJS  
  ```
  System.config({
    map: {
      brolog: 'node_modules/brolog/index.js'
    }
  })
  ```
  
1. import  
  ```
  import { Brolog } from 'brolog'
  ```
    
1. inject to bootstrap  
  ```
  bootstrap(LogApp, [
    Brolog.factory('VERBOSE')
  ])
  ```
  
1. inject to constructor  
  ```
  class LogApp {
    constructor(
      @Inject(Brolog) private log
    ) {
    }
  }
  ```
  
1. log  
  ```
  class LogApp {
    testLog() {
      this.log.verbose('Brolog', 'test log %d', 123)
      // this will log to browser console
    }
  }
  ```

More details, please see the `brolog-angular-demo` git repository [here](https://github.com/zixia/brolog-angular-demo).

# Basic Usage

```
var log = require('brolog')

// additional stuff ---------------------------+
// message ----------+                         |
// prefix ----+      |                         |
// level -+   |      |                         |
//        v   v      v                         v
    log.info('fyi', 'I have a kitty cat: %j', myKittyCat)
```

## log.level()

* {String}

The level to display logs at.  Any logs at or above this level will be
displayed.  The special level `silent` will prevent anything from being
displayed ever.

## log\[level](prefix, message, ...)

* `level` {String} The level to emit the message at
* `prefix` {String} A string prefix.  Set to "" to skip.
* `message...` Arguments to `util.format`

Emit a log message at the specified level.

For example,

* log.silly(prefix, message, ...)
* log.verbose(prefix, message, ...)
* log.info(prefix, message, ...)
* log.warn(prefix, message, ...)
* log.error(prefix, message, ...)

# Reference

1. [JavaScript Modules & Build Tools - YouTube](https://www.youtube.com/watch?v=U4ja6HeBm6s)
2. [Writing Declaration Files](https://www.typescriptlang.org/docs/handbook/writing-declaration-files.html)
3. [Angular Dependency injection tokens](https://angular.io/docs/ts/latest/guide/dependency-injection.html#!#token)
4. [Angular 2 Errors](https://daveceddia.com/angular-2-errors/)
