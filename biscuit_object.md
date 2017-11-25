---
layout: page
title: Biscuit Object
permalink: /biscuit-object/
---

## About

The Biscuit Object is small library in C providing object oriented features for plane C projects.
Source code can be found [here](https://github.com/travisdoor/biscuit_object). BObject is inspired
by [ooc](http://ooc-coding.sourceforge.net/) project created by Tibor Miseta. The original ooc
includes not only OOP tools but also exception handling system, multiple interface inheritance
and other features which I don't want to use so I decided to create my own object system library.

## Motivation
Why not to use C++? After decade spend on mostly C++ projects I realized that I simply don't like
the language complexity which C++ brings. Every new version of C++ allows us to use more and more
sophisticated cool features with horrible syntax and hard readability. I spend more time thinking
about what solution I choose for specified problem than solving those problems directly in simple
way. Finally I found myself doing C with classes in very complex language like C++ so why not to 
use C instead. I don't think that I use C++ wrong way but I think there are too many ways
how to use it and I simply don't like it. 

One of the key features that I miss in C is class model and object system, so I decided to create
this one.

BObject is primary designed for Biscuit Engine where I want to use C# for game-play implementation
and scripting, in this case it is much easier and faster to use C where no wrappers are needed for 
calling "member" functions of the objects living in unmanaged scope.


## Features
- Class definition
- Single parent inheritance 
- Automatic construction and destruction of an object 
- Virtual table and method overriding 
- Runtime virtual method linking 
- New and delete 
- Automatic parent destructor call 

## Other
The Biscuit Object use check unit testing framework and it is fully tested in real solutions and
projects.
