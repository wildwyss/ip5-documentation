---
coverY: 0
---

# Abstract

## Abstract

### Initial situation

At the FHNW  the [Web UI Toolkit Kolibri](https://webengineering-fhnw.github.io/Kolibri/) is being built with contributions from students. The library includes functional abstractions such as those used in the Haskell Standard Library, test support, utilities for secure handling of HTML/DOM, but also development-related aspects.

In this project the Kolibri was extended by further functional abstractions. These abstractions were all presented in a demo application to show how they enrich the Kolibri. Great importance was attached to the quality of the implementation. This quality was ensured by unit tests, user tests and extreme programming. Care has also been taken to write full JSDoc type definitions to assist developers in using the Kolibri.

During the development, the functional aspects of JavaScript such as partial application, higher order functions, pure functions etc. were used to make the implementations more robust, easier to maintain and test.

### Results

The following features were added to the Kolibri Web UI Toolkit in this project:&#x20;

* **Logging Framework**: Developers who are used to the Java programming language often miss the possibility of meaningful logging in JavaScript. Therefore, a new logging framework that offers similar features as [Log4j](https://logging.apache.org/log4j/2.x/) has been built into the Kolibri.
* **Kolibri Iterator**: A data structure that conforms to the [JS Iteration Protocols](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration\_protocols). This data structure has been extended with useful functional concepts like `map` or `filter`.&#x20;
* **Range**: A data structure based on the Kolibri Iterator. This data structure returns a sequence of numbers with arbitrary spacing. Each iteration returns the next element of the sequence.
* **Focus Ring**: An immutable data structure. All elements are arranged in a ring, where one element at a time can be accessed directly (focus). The focus can be moved left or right in the ring.

The usefulness of the developed features was partly already known from other programming languages. Nevertheless, two demo applications were created to show how the abstractions can be used in web development.

In addition, user tests were conducted on the individual topics in order to identify possible problems in the use of the API provided and to obtain opinions of the results from external persons.
