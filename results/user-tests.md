---
description: Evaluation of the user tests
---

# User tests

{% hint style="info" %}
This page describes the results of the user tests. These were conducted in German to make them easier to understand for the participants.
{% endhint %}

## Introduction

To test the implemented abstractions developed during this project more widely, user tests have been performed. Attendees were students and web developers who program on a daily basis and are typical users of constructs similar to those found in the Kolibri Web UI Toolkit.

In order to provide the subjects with a realistic environment, they were presented with a skeleton of a simple web application. This skeleton had some comments in it, which were marked with `TODO`. If all these `TODO` comments were replaced with the corresponding solution, the web application was working in the end. The [skeleton](https://github.com/wildwyss/ip5-usertests/blob/empty-test/userTest.js) and [the final application](https://github.com/wildwyss/ip5-usertests/blob/main/docs/userTest.js) can both be found on Github.

After the programming part, the test persons had to fill out a questionnaire. Assessments of the comprehensibility and usefulness of the frameworks were queried along with basic opinions. The results are discussed below in this document.

The complete application is an image gallery, which uses a Focus Ring and the logging framework. It looks as follows:

<figure><img src="../.gitbook/assets/image (2) (1).png" alt=""><figcaption><p>The probands created an image gallery using the artefacts of this IP5.</p></figcaption></figure>

## Evaluation

The feedback questionnaire was divided according to the implemented abstractions. At the end of the questionnaire, the probands were also allowed to state whether they considered themselves experienced programmers and whether they had knowledge of functional programming. Therefore, about three-fourths think they are experienced and almost all are familiar with functional programming.

### Range

In general, a range did not cause any major problems or incomprehensibility for the probands. This is probably due to the fact that ranges are also known from other programming languages. Most of the test persons think that a range could be useful in a own project. It was also clear to most that a range can be further processed by other operations. So most assume that `map`, `filter` or even `drop` are available.

The following is an evaluation of whether a range would be an asset in a future project:

<figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption><p>Evaluation Range</p></figcaption></figure>

### Focus Ring

The majority of the probands found the Focus Ring to be a simple data structure and think that they are familiar with how this data structure works after performing the programming exercise. All participants see advantages in the fact that the Focus Ring is immutable. More than 75% of them could imagine using this data structure in a future project.

The following is an evaluation of whether a focus ring would be an asset in a future project:

<figure><img src="../.gitbook/assets/image (3) (1).png" alt=""><figcaption><p>Evaluation Focusring</p></figcaption></figure>

### Logging Framework

The basic functionalities of the logging framework were clear to the participants. Simple handling questions were answered correctly by all probands. Most also think that they quickly understood the framework. The configuration of the logger via curried-style is seen a bit more differentiated. Here some have not been able to see the advantage of this implementation and feel this is unnecessarily complicated. However, everyone agrees that the benefits gained by this logging framework justify the slightly more complicated setup. Most could also imagine using the logging framework in their own application.

The following is an evaluation of whether the logging framework would be an asset in a future project:

<figure><img src="../.gitbook/assets/image (5).png" alt=""><figcaption><p>Evaluation Logging-Framework</p></figcaption></figure>

## Conclusion

Basically, we are very happy with the result. Most of the attendees were able to solve the tasks without any major problem. The participants did not always see the advantages of the applied principles, for example the unusual programming style using curried functions. This type of functional programming in JavaScript is rather unfamiliar to many. To make matters worse, some IDEs do not offer the same level of support as for example IntelliJ IDEA does. Therefore the probands have been forced to get a deeper understanding of the code or study the documentation.&#x20;

In general, it has been noticed that good code documentation is central when using a framework or an unknown data structure. This also revealed that subjects without good integration of JSDoc in the IDE had to expend more effort to solve a task.

For us, the most important insight is that the vast majority of subjects find the solutions developed in this project useful and could well imagine them being an asset in a future project.
