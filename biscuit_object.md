---
layout: page
title: Biscuit Object
permalink: /biscuit-object/
---
## About

{: style="text-align: justify;"}
The Biscuit Object is small library in C providing object oriented features for plane C projects.
It is primary designed for Biscuit game engine.
Source code can be found [here](https://github.com/travisdoor/biscuit_object). BObject is inspired
by [ooc](http://ooc-coding.sourceforge.net/) project created by Tibor Miseta. The original ooc
includes not only OOP tools but also exception handling system, multiple interface inheritance
and other features which I don't want to use so I decided to create my own object system library.

## Motivation
- Brings object class structure to plane C.

{: style="text-align: justify;"}
- BObject is primary designed for Biscuit Engine where I want to use C# for game-play implementation
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
- Object creation on stack and heap

## Structure

{: style="text-align: justify;"}
Every custom data type based on BObject type is described by macro-generated static structures (class tables)
containing all informations needed by object instance during execution. Class table contains pointer to class
table of base type (in most cases BObjectKlass table), information about object size, pointers to constructor,
destructor and class initializer, pointer to virtual table (containing virtual method pointers) and object name
as string.

![My helpful screenshot]({{ "/pics/bobject.png" | absolute_url }})

### Boilerplate class definition

{: style="text-align: justify;"}
BObject header contains macros for generating all necessary data types and structures needed by object. Class
table definition and its global instance is created here.

- First block define 'MyObject' derived from 'BObject' fallowed by list of virtual function definitions.

- Second block declare MyObjectParams structure later passed into object constructor.

{: style="text-align: justify;"}
- Third block declare member data of the object. This block could be in separate header file or in implementation
when encapsulation of internal data is needed.

{% highlight c %}
#include <bobject/bobject.h>

/* class MyObject declaration */
/* This will create new class type table and virtual table */
bo_decl_type_begin(MyObject, BObject)
  /* list your virtual functions here */
bo_end();

/* class MyObject constructor params */
bo_decl_params_begin(MyObject)
  /* constructor params goes here */
  int i;
bo_end();

/* class MyObject object data members */
bo_decl_members_begin(MyObject, BObject)
  /* member data */
  int i;
bo_end();
{% endhighlight %}

### Boilerplate class implementation 

{: style="text-align: justify;"}
BObject macro 'bo_impl_type(this, base)' sets all globals needed by type previously defined
in header and also prepare forward definitions for class initializer, constructor, destructor 
and copy constructor methods which must be implemented for every type. 

{: style="text-align: justify;"}
- Class initilializer is called during creation of first instance of 'MyObject' type. Parent
virtual methods can be overridden here.

{: style="text-align: justify;"}
- Constructor is called everytime when 'bo_new' or 'bo_init' is called. 'MyObjectParams' structure
defined previously in class definition is passed here. No validity checking is done on parameter
pack. Constructor of base can be called manually if needed.

{: style="text-align: justify;"}
- Destructor is called before object destruction. Destructors of parent type is called automatically.

- Copy constructor is called when object copy is created.

{% highlight c %}
/* class MyObject */
bo_impl_type(MyObject, BObject);

void
MyObjectKlass_init(MyObjectKlass *klass)
{
  /*
   * Class initialization is called once per type when it is needed.
   * Override virtual functions here.
   */
}

void
MyObject_ctor(MyObject *self, MyObjectParams *p)
{
  /*
   * Constructor
   *
   * Constructor is called for every new object. Set your object
   * data here.
   */

  self->i = p->i;
}

void
MyObject_dtor(MyObject *self)
{
  /*
   * Destructor
   *
   * Destructor is called when object is going to be destroyed.
   * Free all allocated resources here.
   */
  self->i = 0;
}

bo_copy_result
MyObject_copy(MyObject *self, MyObject *other)
{
  /*
   * Copy is called when we're creating this object from another
   * with bo_copy method.
   *
   * Possible return values:
   *  BO_COPY_SUCCESS - copying is done without error
   *  BO_COPY_FAIL    - on error
   *  BO_COPY_DEFAULT - memcpy is used by default for copying other data to self
   *  BO_NO_COPY      - object is non-copyable
   */
  return BO_COPY_DEFAULT;
}
/* class MyObject end */
{% endhighlight %}

### Usage

Example of creating new object on heap.

{% highlight c %}
int main(int argc, const char *argv[]) {
  MyObjectParams p;
  p.i = 666;

  /* create new object instance on heap */
  MyObject *obj = bo_new(MyObject, &p);

  /* delete object */
  bo_delete(obj);
  obj = NULL;

  return 0;
}
{% endhighlight %}

## Other
{: style="text-align: justify;"}
The Biscuit Object use google unit testing framework and it is fully tested in real solutions and
projects.
