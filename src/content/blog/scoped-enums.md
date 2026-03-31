---
title: 'Scoped enums'
description: 'Moving to modern C++'
pubDate: 'Mar 28 2026'
heroImage: '../../assets/blog-placeholder-2.jpg'
---

According to [Meyers](#references), scoped enums are better than unscoped enums.
Unscoped enums are C++98-style enums.
Below is an example from OpenFoam. 

```
//src/thermophysicalModels/reactionThermo/chemistryReaders/chemkinReader/chemkinReader.H
enum phase
{
    solid,
    liquid,
    gas
};
```

why is this ineffective?
why is this unscoped?
Normally, scope is contained within `{}`.
But not in this case. 
`solid`, `liquid`, `gas` are not contained within those braces.
They overflow and pollute the namespace of the class.
That's why I can't have statement like the following.

```
bool solid = false;
```

I should be expecting the following error.
```
chemistryReaders/chemkinReader/chemkinReader.H:81:26: error: 'bool Foam::chemkinReader::solid' conflicts with a previous declaration
   81 |             bool solid = false;
```

### Contain the scope

The magic keyword `class` will make the enum a scoped enum.
```
//src/thermophysicalModels/reactionThermo/chemistryReaders/chemkinReader/chemkinReader.H
enum enum phase
{
    solid,
    liquid,
    gas
};
```
This lets me to use the variables `solid`, `liquid`, `gas` in the namespace where `phase` lives.

### Strongly type

unscoped enums could easily be passed off as `int`s and `float`s.
But not anymore.
One has to explicity cast a scoped enum to use it in the any other context.
This can stop a lot of unforeseen errors.

<!-- Equation 7 in [Bhagatwala, 2015](#references) is the following -->

### References

Meyers, S. (2014). *Effective Modern C++: 42 Specific Ways to Improve Your Use of C++11 and C++14*. O'Reilly Media.