---
description: A Focus Ring for the Kolibri Web UI Toolkit
---

# Focus Ring

{% hint style="info" %}
This section explains how a Focus Ring works internally and how it can be used by developers.
{% endhint %}

## Introduction

### What is a Focus Ring?

A Focus Ring is a data structure in which the elements are arranged as a ring in the outward view. At each point in time, one element of the ring can be accessed with O(1) - this element is called the focus. This focus can be shifted to the left or also to the right. The user of the Focus Ring will therefore never reach an end by moving the focus.

### What can a Focus Ring be used for?

There are many different applications for a Focus Ring. The following are the most common ones:\
To make a selection in a set, may it be date, time, or a month, a concept of a roller is often used. - -Here the Focus Ring can be used to show the currently selected element in focus very easily and scrolling through the other elements can be realized by moving the focus.&#x20;

Probably the best known application for a Focus Ring is an image gallery. In this gallery there is one image in focus, the one the user is currently viewing. To the right and to the left of it, it is usually visually indicated that further images are available. This signals the user that it is possible to navigate to the left or right to view more images.

#### Demo application

Another implementation that uses a focus ring is a slot machine. This slot machine uses three focus rings - one for each reel:

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption><p>A slot machine where each roller is implemented using a Focus Ring.</p></figcaption></figure>

The working slot machine can be tried here: [Slot machine demo application](https://wildwyss.github.io/ip5-sample-applications/contrib/p5\_wild\_wyss/src/focusring/example/SlotMachine.html).

### A Focus Ring for the Kolibri Web UI Toolkit

Based on the concept of the [Kolibri Iterator](iterator.md), a Focus Ring can be implemented with little effort.

## Features

* **Immutability:** The Focus Ring is created as an immutable data structure. That means, a change a of the data structure returns a new object.
* **Direct access:** The focus of the ring can be accessed with O(1).
* **Never ending iteration:** The implementation of the Focus Ring is made in such a way that an end of the elements cannot be reached. Instead, the iteration starts again with the first element.

## Implementation

The Focus Ring is internally implemented with two iterators, which are subsequently called `pre` and `post`. The following figures illustrate the internal handling of the iterators when the focus is shifted several times in one direction. The element that is in focus is always the head element of the `post` iterator and is drawn in purple.

The following figure demonstrates what happens when the focus tried to shift to the right, but no more element is on the right side focus:

<figure><img src="../.gitbook/assets/focus-right.jpg" alt=""><figcaption><p>What happens when the focus is moved right and post has only one element?</p></figcaption></figure>

The following figure demonstrates what happens when the focus tried to shift to the left, but `pre` is empty:

<figure><img src="../.gitbook/assets/focus-left (2).jpg" alt=""><figcaption><p>What happens when the focus is moved left and pre is empty?</p></figcaption></figure>

{% hint style="danger" %}
It is important to note that the `post` side must never be empty. Otherwise no element would be in focus.
{% endhint %}

## Usage

To initialize the Focus Ring a **non-emtpy iterator** is required.

{% hint style="info" %}
Since the Focus Ring is immutable, it must be reassigned for further processing.
{% endhint %}

```javascript
// creates a Focus Ring with the elements from the ArrayIterator
const elems           = ArrayIterator([1,2,3]);
const focusRing       = FocusRing(elems);
  
// the element which is currently in the focus
const focusElement    = focusRing.focus();

// the element to the right or left of the focus
const rightElement    = focusRing.right().focus();
const leftElement     = focusRing.left() .focus();
  
// since the focusring is immutable, it must be reassigned
onst shiftedFocusRing = focusRing.right();
```

## References

| Simon Peyton Jones, A Taste of Haskell - part1 July 23, OSCON 2007: | [https://www.youtube.com/watch?v=jLj1QV11o9g\&t=224s](https://www.youtube.com/watch?v=jLj1QV11o9g\&t=224s) |
| ------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------- |

