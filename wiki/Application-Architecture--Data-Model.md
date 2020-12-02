# Goal

The goal is to create an overall baseline data model spanning over the different fields of user and role model, course structure, file (meta)data model, quizzes, ...

# Course Structure Data Model

![CourseStructureModel](./Images/Architecture/DataModel_CourseStructure.png)

## Description

### Course

The Course is the most important element of this model. The course has a startDate and an endDate. The contained AdjustableTimePeriods can only start and end between those two dates. The Course also contains a maxFoodSum. This is the maximum sum of food that can be earned for the IT-Rex over the entire runtime of the course.

### AdjustableTimePeriod

The AdjustableTimePeriod embodies one period in that a student is supposed to complete a set of chapters. Those chapters can only start and end in the time frame of the AdjustableTimePeriod they belong to. All chapters are supposed to be completed when the AdjustableTimePeriod ends. It also contains a maxFoodSum. The sum of all AdjustableTimePeriods maxFoodSums has to be equal to the maxFoodSum of the Course.

### Chapter

A Chapter is a thematical collection of Contents. A chapter becomes available to the Student when the startDate is reached and is supposed to be completed when the endDate is reached. A Student completes a chapter when all contained Content items have been completed. It also contains a maxFoodSum. The sum of all Chapters maxFoodSums has to be equal to the maxFoodSum of the containing AdjustableTimePeriod.

### Content

A Content item is supposed to be part of a chapter. It becomes available to the student when the startDate is reached and is supposed to be completed when the endDate is reached. It has a foodReward. The sum of all contents foodRewards has to be equal to the maxFoodSum of the containing chapter.

### QuestionPool

The QuestionPool contains all Questions that belong to the course. They can be used in multiple different quizzes.

### ContentPool

The ContentPool contains all Contents that belong to the course. They can be referenced in multiple different chapters this way without uploading them multiple times.

### IdentifiableElement

An IdentifiableElement has a name and an id. The id is used to identify an entity globally.

### TimedElement

A TimedElement has a startDate and an endDate. They describe when the element becomes visible to the Student and when the Student is supposed to complete the Element.

### IT-Rex

IT-Rex becomes hungry when a Content appears. The foodDeficit grows as much as the foodReward of that Content. The foodDeficit can be lowered by feeding IT-Rex. The IT-Rex itself is not destroyed when the course is destroyed because it is supposed to be a permanent trophy for the Student upon the end of the Course.

# Quiz Data Model

![QuizDataModel](./Images/Architecture/DataModel_Quiz.png)

## Description

ToDo
