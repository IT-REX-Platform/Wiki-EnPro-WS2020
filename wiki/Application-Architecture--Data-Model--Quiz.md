# Quiz Data Model

For more information about the design decisions for Quizzes (including setting options, quiz types, etc.) go to [Quizzes](./Quizzes).

![QuizDataModel](./Images/Architecture/DataModel_Quiz.png)

## Description

### IdentifiableElement

An IdentifiableElement has a name and an id. The id is used to identify an entity globally. It is used as a Stereotype on other components.

### Quiz

A Quiz has Questions and can be specified by its QuizSettings. Quizzes are used by LectureQuizzes, RexDuell and TurboQuiz. Remark: When publishing a Quiz the system should check if there is at least one Question associated to it.

### LectureQuiz

It is the most basic Quiz and is also known as "Lehrstandskontrolle". A LectureQuiz tests the knowledge of students about Course content. It can hold Questions with any AnswerType.

### RexDuell

Every Course has exactly one RexDuell. It enables the students to compete with each other by answering Questions about the Course content. It can only access Questions from the QuestionPool of AnswerType 'SingleChoice' that provides exactly four possible answers.

### TurboQuiz

Every Course has exactly one TurboQuiz. It enables the students to learn Course content by answering Quizzes with a time constraint. Because of the time constraint not every Question might be applicable for the TurboQuiz.

### Course

The Course is the central component that contains Quizzes. For further information go to [Course Structure Data Model](./Application-Architecture--Data-Model--Course#course-structure-data-model).

### ContentPool

The ContentPool contains all LecturQuizzes that belong to the Course. Every Course has exactly one ContentPool. For further information go to [Course Structure Data Model](./Application-Architecture--Data-Model--Course#course-structure-data-model).

### QuestionPool

The QuestionPool contains all Questions that belong to the Course. They can be used in all Quizzes, including RexDuell and TurboQuiz (with some restrictions). Every course has exactly one QuestionPool.

### Question

Questions are stored in the QuestionPool and can be used in Quizzes. A Question is defined by its QuestionProperties, its Questioncategories and the AnswerType. It holds the statement of the Question itself which is usually a textual representation but may also include images or other media.

### QuestionCategory

The QuestionCategory is a representation of a lecture Chapter (see [Course Structure Data Model](./Application-Architecture--Data-Model--Course#course-structure-data-model)) and indicates if a Question has a relation to the content of a specific Chapter. There is also a default QuestionCategory if a Question does not fit to a Chapter.

### AnswerType

The AnswerType represents how the Question can be answered. The simplest of these types are shown in the model: SingleChoice, MultipleChoice and Numerical answer.
