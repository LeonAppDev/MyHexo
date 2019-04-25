---
title: TypeScript
date: 2019-03-11 10:25:20
tags:
---

## Implement TypeScript in React

For now if you want to implement TypeScript in a totally new React Project, the best way I think is using React-Create-App <project> --typescript to initialize it

When you introduce it in a existed project, followe instruction in official website, and remember, whenever you want to introduce a new package, check whether it has a type definition, it is better to install a non-typed version with typed defition since react-scripts(When you run the project) may not find the correct path while typesript could find. 

## Fixing some issues

### Absoulte route issue
https://medium.com/@grrowl/fixing-absolute-imports-in-typescript-797f405176eb