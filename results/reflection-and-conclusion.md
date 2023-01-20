# Reflection & conclusion

## Summary

The Kolibri could be extended with the previously documented functionalities. This fulfills the requirements specified in the project description, whereby even more functionality could be implemented. Therefore, the toolkit continues to grow in features and allows programmers who use it to build more stable and robust applications faster and easier. The procedure that led to this result is discussed in the following section. In doing so, the aspects that have been particularly successful and those that we see critical are addressed.

## Collaboration

Basically, the cooperation with our customer and in our team was based on the extreme programming approach. We analyzed the results week by week and determined the next steps on an ongoing basis. This allowed us to focus on specific topics and to build complete and self-contained systems. This approach required us to maintain regular contact with our customer. So, with some exceptions, we met once a week for a meeting that usually took a few hours. The content of this meeting was to discuss the work done so far, to review the code and to define the next steps. This exchange was always enriching for both sides, rich in learning and motivating for further cooperation.

From a technical perspective, we took a test driven approach to our implementation wherever possible. Especially as the code base became more complex, we learned to appreciate this approach and achieved more robust results in less time. Another reason for the successful implementation of the features was the consistent documentation with JSDoc. Only the use of this documentation gives a certain type safety in JavaScript, which pays off with a larger code base.

### What went well?

This section describes some aspects that we intend to maintain in future work. Those gave us structure and confidence that we were on the right track and helped to make the project a success.

Our complete work organization has been orchestrated through a [Notion](https://www.notion.so/) site. This way, we had all the information we needed in a single place. The change history that Notion provides can be accessed by all stakeholders. This also ensures transparency towards the customer / supervisor at all times. During the meetings, a protocol was written in Notion, which always included how to proceed until the next meeting. After each meeting, we created work packages, which we kept on a Kanban board. Based on these work packages, we organized ourself during the next week. It should be mentioned here that a large part of the work was developed in pair programming. For this purpose, independently of the meeting with the customer, we met once a week to work together on the project. During this time, we always made great progress. But at the same time, it was always the most intensive time in which we could benefit and learn from each other.

One of the biggest learning gains came from the regular code reviews at meetings with our supervisor and customer Prof. D. König. At the beginning of a meeting we did a code-walktrough and presented the results we achieved since the last meeting. In the process, we discussed implementation in all aspects: naming, documentation, architecture, code style, paradigms and much more. These conversations were extremely beneficial for learning and one of the most essential parts of this project for us.

To get feedback on our work from uninvolved people, we prepared a user test towards the end of the project. This user test contains a simple project structure in which a structure for an image gallery application is predefined. To create the application, the test persons had to work through several todo's until the application was working. These smaller programming tasks had to be completed with the use of our implemented functionalities of the Kolibri Web UI Toolkit. Subsequently, the participants filled in a questionnaire with some questions concerning the implementations used.

### What can be improved?

In retrospect of our project, we are aware that some aspects can still be improved. Below a few things to focus on in a future project are addressed.

For version management of the code we used a Git repository. For each functionality, i.e. logger, iterator, range and Focus Ring, we have created one branch. In review, we realized that it would have made sense to further subdivide the branches. This would make merge requests smaller and therefore better to look through the code once again before going to `main`. We also see potential for improvement in our commits: In the future, we want to pay more attention to having only one change per commit and to giving it a message that is as meaningful as possible. To better categorize the messages, we want to follow a commit message convention in a next project.

Another point we want to pay attention to is when we document our work. During this project we collected documentation very close to the implementation. As a result, we had to adapt the documentation several times after changes to the code. In the next project, we will keep track of the documentation as soon as one topic is complete in itself. This makes us more efficient and allows us to use the available time more productively.

## Discarded development approaches

In retrospect, we were sometimes on the wrong track. This is normal in the development of software, but should be reflected at this point.

### Logging Framework

At the beginning of the implementation, we fixedly assigned an appender to a logger. This meant that we could neither change the appender nor add more. Originally, the approach was to implement the logger as immutable as possible. However, we had to add an additional state for the appender in the logger. This now allows to remove or add appender during runtime. For more information, consult the [Appender](../technical-documentation/logging-framework.md#appender-1) section.

### Iterator

During the implementation of the iterator, the problem occurred that when copying an iterator, functions already applied to it were not copied as well. In other words, if map was called on an iterator and then copied, the map function was no longer available on the copy. We could solve this problem with a transform function, which is passed to the iterator. At the beginning the function is the id-function. If now a function like map is used on an iterator, the transform function is extended. This happens as described in the section [The Transform Function](../technical-documentation/iterator.md#the-transform-function).

## Conclusion

Above all, it was a great project work for us in which we learned a lot. The most important learning gains for us were the deeper insight into the specification of programming interfaces and how functional programming paradigms in imperative code can help to achieve more robust results.

A special thanks also goes to our coach Prof. Dierk König. In the weekly meetings with him we learned a lot and became much better software developers as a result.
