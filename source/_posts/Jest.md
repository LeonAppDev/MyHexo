---
title: Jest
date: 2019-03-28 11:23:38
tags:
---

## Jest issue on react-natice expo

### failed to cache transform results

I tried uninstall jest-expo, but meet another issue 

``` 
Module react-native/jest/hasteImpl.js in the haste.hasteImplModulePath option was not found.
```

Then I follow the instruction online downgrade jest-expo from '31.0.0' to '29.0.0'.

Then another issue comes

```
 Cannot find module 'setupDevtools' from 'setup.js'

      at Resolver.resolveModule (node_modules/@jest/core/node_modules/jest-resolve/build/index.js:202:17)
      at Object.<anonymous> (node_modules/react-native/jest/setup.js:11:6)
```

The error is because for some reason Jest cannot see the setupDevtools module. To fix, verify that this file is actually in the project, and if it is then your haste/metro cache must be invalid and can't see it.

But I tried everything and can not solve it, so I decided to undo the change in package.json and change whatwg-fetch to 2.0.4 and then remove package-lock.json and node_modules. Then finally this is solved, so my opinion is there are will be inner connection and dependency between packages, and if you just uninstall or install one package, that will break this connection, the fastest solution is to reinstall all of them.


### ReferenceError: self is not defined 

This is an issue caused by 3.0 version of whatwf-fetch, I installed it seperately so it uses newest version
I solve by below step

```
npm uninstall whatwg-fetch
npm i whatwg-fetch@2.0.4 --save

```
You could rm the node_modules and install it again as well. 

### Create mock for fetch

Should be aware Jest is based on node.js, so there is no XMLHttpRequest in Jest, so when test front end project, we need to mock fetch, otherwise Jest will report XMLHttpRequest not find issue