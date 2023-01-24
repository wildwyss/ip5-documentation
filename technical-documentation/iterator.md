---
description: An iterator for the Kolibri Web UI Toolkit
---

# Iterator

{% hint style="info" %}
The basic functionality of an iterator, the possible operations on it and the general usage of the API are considered in-depth in this section.
{% endhint %}

## Introduction

### What is an iterator?

An iterator in JavaScript is an object that is implemented in compliance with the [JavaScript iterator and iterable protocols](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration\_protocols) (henceforth called JS iteration protocols). An iterator is characterized by the fact that it can only be iterated once over a set of elements. After that the iterator is used up.

{% hint style="info" %}
When Kolibri Iterator is mentioned in this chapter, the implementation of the Iterator protocol described **here** is referred to. However, if only iterator is mentioned, iterators in general are meant.
{% endhint %}

#### Iterable vs iterator

In order to be **iterable**, an object must have a property with the key `[Symbol.iterator]`. This property is a function that returns an object containing a function called `next` . The property `[Symbol.iterator]` is called an **iterator**.&#x20;

`next` is a function that returns an object containing two attributes:

* `value`: the value that will be returned next
* `done`: `true` if there are no more values returned by this iterator

### What can an iterator be used for?

An iterator following the JS iteration protocols allows to use `for-of` loops, destructuring assignments and much more on a self created type. This opens up new possibilities in the way programming problems can be solved. Later in this document, a [Range](range.md) using a Kolibri Iterator which is specialized on numbers will be described.

Another advantage of the iterator is that the next element can be calculated. Thus, under certain circumstances, only the current element must be stored. This can significantly increase the storage efficiency.

## Research

When looking at other programming languages, it can be seen that the concept of iterating is probably represented in each one. The approaches to iterators in other programming languages differ mainly in the internal implementation, as well as in the number of the provided functionalities on an iterable object. JavaScript, for example, provides only a few operation on an iterable, whereas Haskell has implemented a more pronounced API.&#x20;

Some concepts are adapted from Haskell during the development of the Kolibri Iterator. To give an example, a function `cons` was implemented analogous to the `cons` operator in Haskell.

The use of the Kolibri Iterator also suits those who are familiar with the Java Stream API.

## Features

### Kolibri Iterator operations

The Kolibri Iterator extends the JS iteration protocols with the following operations:

| Function    | Description                                                                                                                       |
| ----------- | --------------------------------------------------------------------------------------------------------------------------------- |
| `dropWhile` | proceed with the iteration where the predicate no longer holds                                                                    |
| `drop`      | jump over so many elements                                                                                                        |
| `takeWhile` | proceed with the iteration until the predicate becomes true                                                                       |
| `take`      | stop after so many elements                                                                                                       |
| `map`       | transform each element                                                                                                            |
| `retainAll` | only keep elements which fulfill the predicate                                                                                    |
| `rejectAll` | ignore elements which fulfill the predicate                                                                                       |
| `head`      | return the next value without consuming it                                                                                        |
| `isEmtpy`   | returns true, if the iterators head is `undefined`                                                                                |
| `copy`      | duplicate the iterator. If the iterators progress depends on a variable in the closure, copy will not work correctly              |
| `reduce$`   | Performs a reduction on the elements, using the provided start value and an accumulation function, and returns the reduced value. |
| `forEach$`  | executes the callback for each element and exhausts the iterator                                                                  |
| `cons$`     | add the given element to the front of the iterator                                                                                |
| `concat$`   | add an iterator to the existing iterators end                                                                                     |
| `reverse$`  | process the iterator backwards                                                                                                    |
| `eq$`       | checks the equality of two non infinite iterators                                                                                 |

### ArrayIterator

As an extension of the Kolibri Iterator, an `ArrayIterator` is implemented. The `ArrayIterator` enables the usage of the operations mentioned before on arrays.

## Usage

### Creating a Kolibri Iterator

To create a Kolibri Iterator, the constructor function `Iterator` can be used. It takes the following parameters:

| Name                | Type           | Description                                                           |
| ------------------- | -------------- | --------------------------------------------------------------------- |
| `value`             | `T`            | The starting value. The Kolibri Iterator will be initialized with it. |
| `incrementFunction` | `T => T`       | Takes the current value and transforms it to the next.                |
| `stopDetected`      | `T => Boolean` | Detects when the end of an iterator is reached.                       |

{% hint style="warning" %}
For the Kolibri Iterator to work as expected, the following points must be considered:

* `incrementFunction` & `stopDetected` should not refer to any mutable state variable (because of side effects) in the closure. Otherwise, copying an iterator may not work as expected.
* Operations with the `$`-suffix in their names must not be applied to infinite iterators.
{% endhint %}

### Examples

#### Using the `Iterator` constructor

The following example creates a Kolibri Iterator which returns a sequence of numbers starting with 0 up to 99.

{% code lineNumbers="true" %}
```javascript
import { Iterator } from "./iterator/iterator.js";
// create an Iterator
const it = Iterator(0, value => value + 1, value => value < 100);

// process the sequence of numbers
it.retainAll(x => x < 10 || x > 90 )
  .map(x => 10 * x)
  .copy()
  .map(x => x.toString())
  .rejectAll(x => x.length >= 4)
  .takeWhile(x => x !== "90")
  .map(Number)
  .dropWhile(x => x < 40);
```
{% endcode %}

#### Using the `ArrayIterator` constructor

The next example shows how to create an `ArrayIterator` using an array. The `ArrayIterator` then offers all Kolibri Iterator operations on arrays.

{% code lineNumbers="true" %}
```javascript
import { ArrayIterator } from "./iterator/iterator.js";

// create an ArrayIterator
const array = [1,2,3];
const arrayIterator = ArrayIterator(array);

// processing elements by using for-of loop
for (const element of arrayIterator) {
  console.log(element);
}
```
{% endcode %}

## Implementation

### Pre-calculation

When `next` is called for the first time on the Kolibri Iterator, the initial value is returned. However, for the iterator to work correctly, the next value must be calculated each time `next` is called. Thus, the first time the `next` function is called, the second value is generated and remembered, but the previous value is returned.

This way a pre-calculation takes place, in which the next value is calculated in in the present iteration.

### The `transform` function

When using the constructor function `Iterator` a new Kolibri Iterator is created. This function calls a non-exported constructor that takes an additional fourth parameter `transform`, which is initially set to the identity function.&#x20;

This function is a unary operator that is applied to the current element each time `next` is called. The result of `transform` is then returned. Many of the operations implemented on the Kolibri Iterator override the `transform` function to change the iterator.&#x20;

The `transform` operation takes and returns an object of type `TransformType<_T_>`. This object has following attributes:

| Name        | Type      | Description                                                                                                       |
| ----------- | --------- | ----------------------------------------------------------------------------------------------------------------- |
| `done`      | `Boolean` | `true` if the iterator already processed all elements.                                                            |
| `current`   | `any`     | The current transformed value. This could be literally _anything_, depending on all the previous transformations. |
| `nextValue` | `_T_`     | The pre calculated value of the next iteration.                                                                   |

Using these parameters the `transform` function has access to all important information and states of the iterator.

{% hint style="info" %}
Since every Kolibri Iterator depends on an increment and stop detection function which are defined at the start, the real _untransformed_ value must be kept as well. Otherwise the incrementation won't work anymore. This means that in every iteration the untransformed value is increased and kept. Then the transformation is applied.
{% endhint %}

A typical usage of `transform` looks as follows:

1. The previous `transform` function is assigned to a local variable.
2. `transform` is reassigned with a new function.
   1. In the new function the previous `transform` operation is applied.
   2. The functionality of the operation (e.g `filter`, `map`, ...) itself is applied to the result.
   3. The transformed value is returned.

For the operation `map` this looks as follows:

```javascript
  const map = mapper => {
    // 1. remember previous transform operation
    const oldTransform = transform;
    // 2. reassign transform
    transform = x => {
      // 2.1 apply previous transformation
      const  { done, current, nextValue } = oldTransform(x);
      // 2.2 & 2.3 apply map operation and return the next value.
      return { done, current: mapper(current), nextValue };
    };
    return iteratorObject;
  };
```

### Naming

Some functions defined on the Kolibri Iterator also work with infinite sequences. Thus infinite data streams can be generated. However some operations on the iterator are not able to handle infinite iterators. For example the `reverse$` operation needs to process all elements.

Functions that only work with finite sequences are marked with a `$` sign at the end of their names. The dollar sign was chosen because it also marks the end of a line in regex expressions.

## Future features

This section describes further features that could extend the Kolibri Iterator.

| Feature                           | Description                                                                                               |
| --------------------------------- | --------------------------------------------------------------------------------------------------------- |
| Improve `retainAll` & `rejectAll` | Simplify the implementation of `retainAll` & `rejectAll` using `dropWhile`.                               |
| Additional constructor            | A curried style constructor for the iterator.                                                             |
| `tail$`                           | Returns the last element and drops it.                                                                    |
| `uncons`                          | Removes the head from a list and returns it.                                                              |
| `mapIndexed`                      | Pass the index as well into the mapper.                                                                   |
| `find`                            | Returns the first element which fulfills a given predicate.                                               |
| `count$`                          | Returns the number of all elements.                                                                       |
| `max$`                            | The max item of all elements.                                                                             |
| `min$`                            | The min item of all elements.                                                                             |
| `zip`                             | Combines two Kolibri Iterators and returns an Iterator of corresponding pairs.                            |
| `zipWith`                         | Generalizes `zip` using an arbitrary mapping function to create the new elements of the Kolibri Iterator. |
| `zipWithIndex`                    | Adds the index to each element of the Kolibri Iterator.                                                   |
| `sort$`                           | Sorts all elements by a given function.                                                                   |

## References

| JS iteration protocols                            | [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration\_protocols](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration\_protocols)                           |
| ------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Visualization of many Kolibri Iterator operations | [https://rxmarbles.com/](https://rxmarbles.com/)                                                                                                                                                           |
| `cons` operator in Haskell                        | [https://hackage.haskell.org/package/bytestring-0.11.3.1/docs/Data-ByteString-Lazy-Char8.html#v:cons](https://hackage.haskell.org/package/bytestring-0.11.3.1/docs/Data-ByteString-Lazy-Char8.html#v:cons) |

