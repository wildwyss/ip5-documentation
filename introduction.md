# Introduction

## Problem statement

In this IP5, several solutions known from functional programming languages are adapted to JavaScript. These functional solution approaches bring various advantages such as better clarity, maintainability and easier verifiability through unit tests.

JavaScript, which already implements many concepts of functional programming at its core, is thus supplemented by further suitable constructs. The usefulness of these constructs are ensured by user tests.

The quality of the results, documentation and tests are very important.

## Results

The final artifacts of this IP5 are realized as parts of the [Kolibri Web UI Toolkit](https://webengineering-fhnw.github.io/Kolibri/) (henceforth called Kolibri). The project work can be divided into two parts:&#x20;

1. Logging framework&#x20;
2. Functional data structures

These two parts are roughly paraphrased as part of this introduction. More detailed information about the implementation and usage can be found in the following chapters.

### Logging Framework

JavaScript offers the possibility to log to the web console. However, important features like log priorities or logging to other targets are not supported. For example, it is impossible to collect and evaluate logs. Finding errors in runtime is also very difficult with the existing possibilities.

When addressing the logging framework for the Kolibri, the following is considered:

* Easy extension and configuration of the framework
* Simple use of the configured framework

### Functional data structures

In JavaScript there is a definition called [JS iteration protocols](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration\_protocols). Constructs that conform to these protocols are called iterators and provide a way to generate values. In addition, JavaScript provides convenient language features that make iterators even more attractive.

#### Kolibri Iterator

However, there are no operations defined in the iteration protocols that provide further processing of the values. Therefore, these are implemented in a first step. Which operations these are, is explained in the section [Iterator](technical-documentation/iterator.md).

#### Range

A range builds on a Kolibri Iterator and, like ranges in other programming languages, returns numerical values between two boundaries. All operations that are available to the Kolibri Iterator are also available to the range.

#### Focus Ring

The Focus Ring is a simple, immutable data structure whose elements are arranged in a ring. One element at a time is in focus and can be accessed with O(1). The focus can be shifted one place to the left or right.

### Demo applications

The logging framework is demonstrated as a UI logger. Each log statement is displayed directly on the UI. This demonstrates the extensibility of the framework. A running demo can be found [here](https://wildwyss.github.io/ip5-overview/contrib/p5\_wild\_wyss/src/logger/logUi/example/logUiExampleView.html).

To demonstrate the Focus Ring (and thus also the Range and the Kolibri Iterator) a slot machine was built that has three rollers. Each of these rollers is implemented using a Focus Ring. Following is a picture of the [sample application](https://wildwyss.github.io/ip5-overview/contrib/p5\_wild\_wyss/src/focusring/example/SlotMachine.html).

<figure><img src=".gitbook/assets/image (2) (1).png" alt=""><figcaption><p>The slot machine shows how Focus Rings can be used.</p></figcaption></figure>



## Methodology

Because this IP5 is not a typical implementation project, but a research project, the outcome of the implemented artifacts is open at the beginning. Therefore, the process of approaching the task is also different. For this reason, it is more difficult to estimate the results based on the task. In order to ensure and evaluate the progress of the work nevertheless, an incremental approach to solve the problem statement is taken. This incremental progress was assessed through weekly site reviews. Based on this evaluation, the goals for the next work steps have been defined.

## Readers guide

[The next section](technical-documentation/) covers the technical details and implementation of this IP5 in-depth. It gives an understanding how the artefacts developed in this project work and how they can be used within other projects.

Readers interested primarily in the results are referred directly to the [Results](introduction.md#results) section at this point.

## References

| Project description | [22HS\_IMVS37](https://wildwyss.github.io/ip5-overview/22HS\_IMVS37%20Funktionale%20Standard%20Library%20f%C3%BCr%20das%20Kolibri%20Web%20UI%20Toolkit.pdf) |
| ------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
