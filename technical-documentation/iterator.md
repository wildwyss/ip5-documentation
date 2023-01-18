---
description: An Iterator for the Kolibri Web UI Toolkit
---

# Iterator

{% hint style="info" %}
The basic functionality of an iterator, the possible operations on it and the general usage of the API are considered in depth.
{% endhint %}

## Introduction

### What is an Iterator?

An iterator is basically an object that is implemented in compliance with the [JavaScript iterator and iterable protocols](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration\_protocols). An iterator is characterized by the fact that it can only be iterated once over a set of elements. After that the iterator is used up.

In order to follow the iterator protocol, it is mandatory that the object that should represent an iterator returns a property with the name `[symbol.iterator]`. This property is a function that returns an object containing a `next` and a `done` attribute. `next` is a function that returns the next element above the set being iterated on. This continues until the `done` attribute is true, which is also contained in the object.

### What can an Iterator be used for?

An iterator following the [JavaScript iterator and iterable protocols](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration\_protocols) now allows to implement for-of loops, destructering and much more on a self created data type. This opens up new possibilities in the way programming problems can be solved. Later in this document, a [Range](range.md) using a Kolibri Iterator specialized on number will be described.

Another advantage of the iterator is that the next element can be calculated. Thus, under certain circumstances, only the current element must be stored. This can significantly increase the storage efficiency.

## Research

If you look at other programming languages, you can see that the concept of iterating is probably represented in each one. Thus the programming languages differ mainly in the internal implementation, as well as in the number of the provided functionalities on an iterable object. JavaScript, for example, provides only a few functions on an Iterable, whereas Haskell has implemented a more pronounced API.&#x20;

Some concepts could also be adapted from Haskell during the development of this Kolibri Iterator. To give an example, a function `cons` was implemented analogous to the `cons` operator in Haskell.&#x20;

The use of the Kolibri Iterator should also suit those who are familiar with Java Stream.

## Features

### Iterator functions

The following are the functionalities implemented in the Kolibri Iterator.

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
| `isEmtpy`   | returns true, if the iterators head is undefined                                                                                  |
| `copy`      | duplicate the iterator. If the iterators progress depends on a variable in the closure, copy will not work correctly              |
| `reduce`$   | Performs a reduction on the elements, using the provided start value and an accumulation function, and returns the reduced value. |
| `forEach$`  | executes the callback for each element and exhausts the iterator                                                                  |
| `cons$`     | add the element to the front of the iterator                                                                                      |
| `concat$`   | add an iterator to the existing iterators end                                                                                     |
| `reverse$`  | process the iterator backwards                                                                                                    |
| `eq$`       | checks the equality of two non infinite iterators                                                                                 |

### ArrayIterator

As an extension of the Kolibri Iterator, an `ArrayIterator` was implemented. The `ArrayIterator` enables the usage of the functions mentioned before on arrays.

## Implementation

### Creating a Iterator

To create an iterator, an initial value and two functions are needed, which are described below.

#### value

The start value with that the iterator is initialized.

#### increment function

The increment function is passed to the iterator and takes care internally how to get from the current value to the next. It is important that this function makes a progress towards the stopFunction described below.

#### stopDetected

The stopDetection Function detects when the end of an iterator is reached. This is a predicate.

### Naming

Some functions on the iterator also work with infinite rows. Thus infinite data streams can be generated. However, because functions are also implemented on the iterator, such as the comparison of whether two iterators are equal, which cannot handle infinite data streams, these had to be specially marked. For this purpose these functions are marked with a `$` dollar sign. The dollar sign was chosen because it also marks the end of a line in regex expressions.

## Usage

### Contract

For the iterator to work as expected, the following points must be considered:

* IncrementFunction & stopDetected should not refer to any mutable state variable (because of side effect) in the closure. Otherwise, copying and iterator may not work as expected.
* Functions ending with a "$" must not be applied to infinite iterators.

### Iterator Example

{% code lineNumbers="true" %}
```javascript
// create an Iterator
const it = Iterator(0, value => value + 1, value => value < 100);

// process the stream of numbers
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

### ArrayIterator Example

{% code lineNumbers="true" %}
```javascript
// create an ArrayIterator
const array = [1,2,3];
const arrayIterator = ArrayIterator(array);

// processing elements by using for-of loop
for (const element of arrayIterator) {
  console.log(element);
}
```
{% endcode %}

## References

| Author | Source                                                                                                                                                                                                     |
| ------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
|        | [https://rxmarbles.com/](https://rxmarbles.com/)                                                                                                                                                           |
|        | [https://hackage.haskell.org/package/bytestring-0.11.3.1/docs/Data-ByteString-Lazy-Char8.html#v:cons](https://hackage.haskell.org/package/bytestring-0.11.3.1/docs/Data-ByteString-Lazy-Char8.html#v:cons) |
|        |                                                                                                                                                                                                            |
