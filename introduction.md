# Introduction

## Results

The final artifacts are realized as part of the Kolibri Web UI Toolkit and are future components of this toolkit. The IP5 work can be roughly divided into two parts:&#x20;

1. Logging framework&#x20;
2. Functional data structures

These two parts are roughly paraphrased as part of this introduction. More detailed information about the implementation can be found in the following chapters.

### Logging Framework

JavaScript offers the possibility to log to the JS console. However, important features like log priorities or logging to other targets are not supported. For example, it is impossible to evaluate logs. Finding errors in runtime is also very difficult with the existing possibilities.

When addressing the logging framework for the Kolibri, the following is considered:

* Easy extension and configuration of the framework
* Simple use of the configured framework

### Functional data structures

In JavaScript there is a definition called JS Iteration Protocols. Constructs that conform to the Iteration Protocols are called iterators and provide a way to generate values. In addition, JavaScript provides convenient language features that make iterators even more attractive.

#### Kolibri Iterator

However, there are no functions for the iteration protocols that provide further processing of the values. These are implemented in a first step. Which operations these are, is explained in the section Iterator.

#### Range

A Range builds on a Kolibri iterator and, like ranges in other programming languages, returns numerical values between two boundaries. All operations that are available on the Kolibri Iterator are also available on the Range.

#### Focus Ring

The Focus Ring is a simple, immutable data structure whose elements are arranged in a ring. One element at a time is in focus and can be accessed with O(1). The focus can be shifted one place to the left or right.

### Demo applications

The logging framework is demonstrated as a UI logger. Each log statement is displayed directly on the UI. This demonstrates the extensibility of the framework. A running demo can be found [here](https://wildwyss.github.io/ip5-sample-applications/contrib/p5\_wild\_wyss/src/logger/logUi/example/logUiExampleView.html).

To demonstrate the Focus Ring (and thus range and iterator) a slot machine was built that has three rollers. Each of these roles is implemented by a Focus Ring. A running demo can be found [here](https://wildwyss.github.io/ip5-sample-applications/contrib/p5\_wild\_wyss/src/focusring/example/SlotMachine.html).

<figure><img src=".gitbook/assets/image (2).png" alt=""><figcaption><p>The slot machine shows how Focus Rings can be used.</p></figcaption></figure>

## Problem statement

In this IP5 project, several solutions known from functional programming languages are adapted to JavaScript. These functional solution approaches bring various advantages such as better clarity, maintainability and easier verifiability through unit tests.

JavaScript, which already implements many concepts of functional programming at its core, is thus supplemented by further suitable constructs. The usefulness of these constructs are ensured by user tests.

The quality of the results, documentation and tests are very important.

## Readers guide

[The next section](technical-documentation/) covers the technical details and implementation of this IP5 in-depth. It gives an understanding how the artefacts developed in this project work and how they can be used within other projects.

Readers interested primarily in the results are referred directly to the [Results](introduction.md#results) section at this point.
