---
description: Evaluation of the user tests
---

# User tests

{% hint style="info" %}
This page describes the results of the user tests.
{% endhint %}

## Introduction

To test the implemented abstractions more widely, we performed user tests. Our probands were all students who program on a daily basis and are typical users of implementations like the one we implemented.

We have created a JavaScript file for this purpose, which contains some prepared tasks. For this purpose, a basic structure of an application was created in the code and where the test person had to program something supplementary, a task was described and marked with a TODO.

After the programming, the test persons had to fill out a questionnaire. Assessments of the comprehensibility and usefulness of the frameworks were queried along with basic opinions. The results are discussed below in this document.

## Evaluation

The feedbacks were divided according to the implemented abstractions. At the end of the questionnaire, the probands were also allowed to state whether they considered themselves experienced programmers and whether they had knowledge of functional programming. Therefore, about three-fourths think they are experienced and almost all are familiar with functional programming.

### Range

In general, a range did not cause any major problems or incomprehensibility for the subjects.This is probably due to the fact that a range is also known from other programming languages. Most of the test persons think that a range could be used in a own project.It was also clear to most that a range can be further processed as an iterable. So most assume that map, filter or even drop are available.

### Focusring

DThe majority of the probands found the focus ring to be a simple data structure and think that they are familiar with how this data structure works after performing the programming exercise. All participants see advantages in the fact that the focus ring is immutable.Almost all of them could imagine using this data structure in a future project.

### Logging Framework

The basic functionalities of the logging framework were clear to the participants. Simple handling questions were answered correctly by all probands. Most also think that they quickly understood the framework. The configuration of the logger via curried-style is a bit more differentiated. Here some have not been able to see the advantage of this implementation and feel this is unnecessarily complicated. However, everyone agrees that the benefits gained justify the slightly more complicated setup. Most could also imagine using the logging framework in their own application.

## Conclusion

Basically, we are very happy with the result. Most of them were able to solve the tasks without any major problems. The participants had somewhat more difficulty in recognizing the advantages of the principles applied. We attribute this to the unusual programming style used in curried-style, for example. This type of functional programming is rather unfamiliar to many. To make matters worse, the IDE does not offer the same level of support and you are forced to get a deeper understanding of the code or study the documentation. In general, it has been noticed that good code documentation is central to the use of a framework or data structure. This also revealed that subjects without good integration of the jsDoc in the IDE had to expend more effort to solve a task.
