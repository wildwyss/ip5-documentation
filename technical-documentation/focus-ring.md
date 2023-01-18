---
description: A Focus Ring for the Kolibri Web UI Toolkit
---

# Focus Ring

{% hint style="info" %}
This section explains how a focus ring works internally and how it can be used by developers.
{% endhint %}

## Introduction

### What is a Focus Ring?

A Focus Ring is a data structure in which the elements are arranged as a ring in the outward view. At each point in time, one element of the ring is in focus. This focus can be shifted to the left or also to the right. The user of the Focus Ring will therefore never reach an end by moving the focus.

### What can a Focus Ring be used for?

There are many different applications for a Focus Ring. The following are the most common ones:\
To make a selection in a set, may it be date, time, or a month, a concept of a roller is often used. - -Here the Focus Ring can be used to show the currently selected element in focus very easily and scrolling through the other elements can be realized by moving the focus. One kind of this application was implemented as [an example with a slot machine](https://github.com/wildwyss/Kolibri/tree/feature/range/contrib/p5\_wild\_wyss/src/focusring/example).&#x20;

Probably the best known application for a Focus Ring is an image gallery. In this gallery there is one image in focus, the one the user is currently viewing. To the right and to the left of it, it is usually visually indicated that further images are available. This signals the user that it is possible to navigate to the left or right to view more images.

### A Focus Ring for the Kolibri Web UI Toolkit

Based on the concept of the [iterator](iterator.md), a Focus Ring can be implemented relatively easily. As described in the previous section, the Kolibri Web Ui Toolkit has been extended to allow the use of [iterators](iterator.md) in JavaScript. Thus it is obvious to provide the Kolibri Web Ui Toolkit with a Focus Ring.

## Features

* **Immutability:** The Focus Ring is created as an immutable data structure. That means, a change a of the data structure returns a new object.
* **Never ending iteration:** The implementation of the Focus Ring is made in such a way that an end of the elements cannot be reached. Instead, the iteration starts again with the first element.

## Implementation

The Focus Ring is internally implemented with two iterators, which are subsequently called pre and post. The following figure illustrates the internal handling of the iterators. One element is always in focus. This is the head element of the post iterator and is marked in purple. The two process flows that demonstrate the shifting to the right and left are listed below each other in the graphic. The special cases are to be considered in each case, if a side, thus pre or post, becomes empty. Then the opposite side is taken and added upside down.

<figure><img src="../.gitbook/assets/Focusring demo.png" alt=""><figcaption><p>Internal Focus Ring handling</p></figcaption></figure>

{% hint style="info" %}
It is important to note that the post side must never be empty. Otherwise no element would be in focus.
{% endhint %}

## Usage

To initialize the Focus Ring a **non-emtpy iterator** is required.

{% hint style="warning" %}
Since the Focus Ring is immutable, it must be reassigned for further processing.
{% endhint %}

```javascript
  // creates a Focus Ring with the elements from the ArrayIterator
  const elems     = ArrayIterator([1,2,3]);
  const focusRing = FocusRing(elems);
  
  // the element which is currently in the focus
  const focusElement     = focusRing.focus();
  
  // the element to the right or left of the focus
  const rightElement     = focusRing.right().focus();
  const leftElement      = focusRing.left() .focus();
  
  // since the focusring is immutable, it must be reassigned
  const shiftedFocusRing = focusRing.right();
```

## References

| Author                                                              | Source                                                                                                     |
| ------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------- |
| Simon Peyton Jones, A Taste of Haskell - part1 July 23, OSCON 2007: | [https://www.youtube.com/watch?v=jLj1QV11o9g\&t=224s](https://www.youtube.com/watch?v=jLj1QV11o9g\&t=224s) |

