---
description: Testing and documentation
---

# Quality assurance

{% hint style="info" %}
This page describes how the quality of this project is assured through testing and documentation.
{% endhint %}

## Introduction

To keep the quality of the artefacts of this project as high as possible, the following points have been considered:

* Achieve high test coverage
* Prevent code duplication
* Purpose and types of functions and objects are documented in the source code
* Split code into multiple modules
* Perform code reviews

In the following, the most important points are explained in more detail. These contribute significantly to quality assurance during development.

## Testing

A test-driven approach was used where possible. In addition, care has been taken to ensure that every feature is tested. To achieve this, the [Kolibri test suite](https://github.com/WebEngineering-FHNW/Kolibri/blob/main/docs/src/kolibri/util/test.js) was used, which was already implemented in the toolkit.

### Benefits

Functioning tests are extremely useful during development. It gives a certain safety when things are changed or added. Finally, by using tests, progress is greater because bugs and inconsistencies can be found more quickly.

### Usage

This test framework is very easy to use and provides a good overview of successful and failed tests.

Below is a screenshot of the summary of all implemented tests written during the project. To organize the tests, each feature has its own test suite.

<figure><img src="../.gitbook/assets/image (6).png" alt=""><figcaption><p>Test Summary</p></figcaption></figure>

## Code documentation

### Benefits

The whole code base is documented with JSDoc. Thus, the untyped language JavaScript can be supplemented with a working type safety. JSDoc is well supported by modern IDEs like IntelliJ. This helps with the implementation but also with the use of the source code.

Furthermore, parameters, types and functions can be described in more detail in the code. This is very beneficial for users of the implementations and helps to significantly improve the understanding of the code.

### Conventions

In order to achieve good consistency, existing naming concepts from the Kolibri were adopted. For this purpose, the following types are written in UpperCamelCase notation:

* **Callbacks**: Callbacks are functions that are passed to another function.&#x20;
* **Constructor Functions**: Functions that create objects are called constructors.

To prevent code duplication, types are kept as generic as possible. As an example, callback types have been created analogous to those known from the Java functional interfaces. Each feature has it's type definition in a separate file named `types.js`. An example can be found [here](https://github.com/wildwyss/Kolibri/blob/main/contrib/p5\_wild\_wyss/src/types.js).

### Example

The following example shows a detailed description of the range constructor. It is easy to see that special behaviors, which may not be intuitive for everyone, can be described well.

```javascript
/**
 * Creates a range of numbers between two inclusive boundaries,
 * that implements the iterator protocol.
 * First and second boundaries can be specified in arbitrary order,
 * step size is always the third parameter.
 * Consider the examples at the end of the documentation.
 *
 * Contract:
 * - End-value may not be reached exactly, but will never be exceeded.
 * - Zero step size leads to infinite loops.
 * - Only values that behave correctly with respect to addition and
 *   size comparison may be passed as arguments.
 * @constructor
 * @param { !Number } firstBoundary  - the first boundary of the range
 * @param { Number }  secondBoundary - optionally the second boundary of the range
 * @param { Number }  step - the size of a step, processed during each iteration
 * @returns IteratorType<Number>
 * @example
 *  const [zero, one, two, three] = Range(3);
 *  const [five, three, one]      = Range(1, 5, -2);
 *  const [three, four, five]     = Range(5, 3);
 */
const Range = (firstBoundary, secondBoundary = 0, step = 1) => {
  const stepIsNegative = 0 > step;
  const [left, right]  = normalize(firstBoundary, secondBoundary, stepIsNegative);

  return Iterator(
    left,
    value => value + step,
    value => hasReachedEnd(stepIsNegative, value, right)
  );
};
```

## References

| Java - Functional Interfaces                             | [https://docs.oracle.com/javase/8/docs/api/java/util/function/package-summary.html](https://docs.oracle.com/javase/8/docs/api/java/util/function/package-summary.html) |
| -------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| IP6-Documentation including the Test Framework (Page 61) | [https://dierk.github.io/Home/data/IP6\_Bericht\_Misic\_H%C3%A4fliger.pdf](https://dierk.github.io/Home/data/IP6\_Bericht\_Misic\_H%C3%A4fliger.pdf)                   |
| JSDoc Homepage                                           | [https://jsdoc.app/](https://jsdoc.app/)                                                                                                                               |
