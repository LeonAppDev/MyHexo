---
title: Prototype in Javascript
date: 2019-02-13 10:28:46
tags:
---

## What is prototype
   In Javasript, there are two concepts which is quite confused, one is prototype and the other is __proto__, but they are quite different. prototype is actually an object which has a property named constructor. and only original object has prototype. When you create any object from an original object, javasript will assign properties in prototype. \__proto\__ is a property in Object.prototype, since Object is the root object for any other, object, so any other object will get this property. Then javascript will assign \__proto\__ of the new object with upper level original object's prototype. 

## Function and Object
   In javacript, Function and Object is one thing with different feature. Function is the original of all functions and Object is the original of all objects.
   And Function could aslo have feature of object and Object could aslo be a function. So when you refer to Function, you need to figure out whether you refer to its function feature or its object feature.  
   Function and object are bind together is 