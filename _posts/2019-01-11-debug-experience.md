---
layout:     post
title:      "Debug Experience"
subtitle:   "代码除错经验"
date:       2019-01-11
author:     "starwavelin"
header-img: "img/post-banner/post-bg-debug.jpg"
tags:
    - Extensible Note
---

### 2019 Jan 4
**Why sometimes we don’t want to return a promise, instead just calling a promise?**   
ie.
```
return selection.save().then(() => {
    const action = selection.checked ? Action.BadActionChecked : Action.BadActionUnchecked;
    this.recordAction(action, selection.name);
  });
```
Here, we don't `return this.recordAction(action, selection.name);` and just called `this.recordAction(action, selection.name);`  

This is because: here we don't want to return the function call in purpose; we don't want the `recordAction()` in case break and delay the original logic. Without `return`, it will be fired but without changing any original logic.

**Some Amorphic thing: set 2nd level property dirty**  
If you modify the second level property of an object, you also need to setDirty for the 2nd level property as well as the first-level property. ie.
```
const dept = this.SBU.dept;
dept.major.courseOffering = CourseOfferingList.Selected;
// 1st level property: dept itself; 2nd level property: dept.major
// ......
ApplicationContext.get.executionContext.trans.setDirty(dept.major); // set 2nd level property dirty first
ApplicationContext.get.executionContext.trans.setDirty(dept); // then set 1st level property (obj itself)
```
But, the above is necessary only when you want to save both the `major` object and `dept` object. If in any case you just want to save the `major` object, and the `dept` object only holds the `major_id`, which means the change of the content of `major` will not trigger any change of the `dept` object, then, you just need to do   
```
ApplicationContext.get.executionContext.trans.setDirty(dept.major); // set 2nd level property dirty
```

### 2019 Jan 3
Error Message
```
==== JS stack trace =========================================

    0: ExitFrame [pc: 0x1fd2ddd041bd]
Security context: 0x13f173f9e6c9 <JSObject>
    1: createPropertyAccess [0x13f16d905081] [/starwavelin/tadex/node_modules/typescript/lib/tsc.js:~40892] [pc=0x1fd2debe463d](this=0x13f10fe8fdf9 <Object map = 0x13f15c5f2da9>,expression=0x13f11bf7b189 <Node map = 0x13f15c5ed081>,name=0x13f11bf7b221 <Node map = 0x13f198e17d89>)
    2: substituteExpressionIdentifier(aka substituteExpressi...

FATAL ERROR: Ineffective mark-compacts near heap limit Allocation failed - JavaScript heap out of memory
```

What happened? When I was adding some test case files (.ts files), the ts to js compiler encountered heap out of memory (OOM) error. By doing some research, I figured out two ways to solve it. And these two ways can be used in combination.

*Solution 1*  
By issueing this command `./node_modules/.bin/tsc --diagnostics`, I know compilation already took about 1.4GB memory. And gradually adding .ts files, I saw the compilation passed a certain threshold that caused this error. Doing research online, as [this article](https://discourse.nativescript.org/t/avoiding-out-of-memory-errors-with-tsc-typescript-compiler/1081) pointed out, the default memory for compilation is 1.7GB, and split this memory to heap and stack, it is reasonable that heap OOM may happen when passing a threshold like 1.5GB.  
So, I can update the `node_modules/typescript/bin/tsc` from  
```
#!/usr/bin/env node   

require('../lib/tsc.js')
```
into
```
#!/usr/bin/env node --max-old-space-size=2048   

require('../lib/tsc.js')
```
Just append `--max-old-space-size=2048` into the line with `#!`, it will take effect.  

But this solution has a flaw. Because any time when we do `$ npm i`, the change in this `tsc` file within the `node_modules` folder will disappear. This lead to my 2nd solution.

*Solution 2*  
To bypass the flaw in Solution 1, I need to put `--max-old-space-size=2048` in some file like `tsconfig.json` or `package.json`, ultimately I know `package.json` is the right place.   
So I can do something in `package.json` like below  
```
"tsc": "node --max-old-space-size=2048 ./node_modules/typescript/lib/tsc.js -p ./tsconfig.json"
```
And then I further realize that the initial cause of this OOM was due to adding more .ts files for tests, and these regression tests **don not** need to be in our production environment. Then, why not split regular .ts source code compilation from the test file compilation? Hence, I do  
```
"tsc": "npm run tsc:apps && npm run tsc:tests",
"tsc:apps": "node --max-old-space-size=2048 ./node_modules/typescript/lib/tsc.js -p ./tsconfig.json",
"tsc:tests": "node --max-old-space-size=2048 ./node_modules/typescript/lib/tsc.js -p ./tsconfig-tests.json",
```
This guarantees the compilation memory consumption is much lower than 1.4GB for compiling test files, and even if the source file addition is growing in the future, we already have increase the limit for the compilation memory from 1.7GB to 2.0GB.

Some useful CL (command line) commands I learned in Mac:
```
$ top -u              # sort processes by memory consumption from higher to lower
$ top -u | grep node  # cuz it was node.js program caused OOM, so grep by node
```
