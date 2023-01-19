---
description: Testing and Documentation
---

# Quality assurance

{% hint style="info" %}
This page describes how we implemented testing and documentation in the code.
{% endhint %}

## Introduction

To keep the quality of the source code as high as possible, we paid attention to the following points:

* achieve high test coverage
* prevent code duplication
* purpose and type is documented in the source code
* split code into multiple files
* perform code reviews

In the following, we would like to discuss individual points that have been especially helpful to us during the project.

### Testing

Where possible, we have taken a test-driven approach. Besides that, it was important to us that every feature is tested. To achieve this, we used the Kolibri Test-Suite, which was already implemented in the toolkit. You can find the source code [here](https://github.com/WebEngineering-FHNW/Kolibri/blob/main/docs/src/kolibri/util/test.js).

#### Benefits

Functioning tests are extremely useful during development. It gives a certain safety when things are changed or added. Finally, by using tests, progress is greater because bugs and inconsistencies can be found more quickly.

#### Usage

This test framework is very easy to use and provides a good overview of successful and failed tests.

Below you can see a screenshot of the summary of our written tests. To organize the tests we used separate test suites for each feature. This allows for a differentiated view.

<figure><img src="../.gitbook/assets/image (6).png" alt=""><figcaption><p>Test Summary</p></figcaption></figure>

### Code documentation

#### Benefits

To write robust and sustainable code we used jsDoc. This allows to introduce a kind of type system for JavaScript. The IDE can detect if you are working with the right types. This helps with the implementation but also with the use of the source code.

Furthermore, parameters , types and functions can be described in more detail in the code. This is very beneficial for users of the implementations and helps to significantly improve the understanding of the code.

#### Conventions

To achieve good consistency, we have adopted existing concepts from the Kolibri Web Ui Toolkit. For this purpose, the following types are capitalized.

* **Callbacks**: Callbacks are functions that are passed to another function. Their type is written in capital letters.
* **Constructor Functions**: Functions that create an object are called constructors and are written in capital letters.

To prevent code duplication, we have tried to keep the types as generic as possible. For example, we implemented some callbacks that are known as Functional Interfaces in Java. These types, which could be kept generic and are not only used in a special context, are stored in a seperate file. Such a file is named with `types.js` and can be found for example [here](https://github.com/wildwyss/Kolibri/blob/main/contrib/p5\_wild\_wyss/src/types.js).

#### Example

In the following example you can see a detailed description of the range. It is easy to see that special behaviors, which may not be intuitive for everyone, can be described well.

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
| jsDoc Homepage                                           | [https://jsdoc.app/](https://jsdoc.app/)                                                                                                                               |
