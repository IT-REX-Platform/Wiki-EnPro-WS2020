# Publishing and Lifecycle

The general idea is that any content in IT-REX follows a predefined lifecycle instead of just being "CREATED" or "DELETED". The rationale is to enable lecturers to upload contents and prepare them, before making them accessible by students. And to allow students to rely on published material being unchanged without them noticing it, hence offering lecturers the opportunity to purpusefully upload updates to already published contents. Consequently, contents can only be delted after they have been marked as archived - unless they haven't been published yet.

In the following, we want to give an overview about the publishing process and the lifecycle for [Courses](#Course-Lifecycle) and [Course Contents](#course-content-lifecycle). This process is only partially implemented, but draws the vision of content management in IT-REX.

| :warning: The implementation of contents in a course was realized using the entity "ContentReference" as an abstraction,  mapping the actual content (e.g., the video), to a position in a course chapter. This detail is not regarded here, i.e., there is no differentiation between contents and content references from the lifecycle perspective. Both the content item and content reference management must be implemented in a way that follows the specified lifecycle. |
|---|

## Course Lifecycle

Courses should follow the following lifecycle. When courses are PUBLISHED, students can join them. Courses can only be deleted after being archived, which can be used to implement a time period that is required to pass before transitioning from ARCHIVED to being deleted.

UNPUBLISHED courses can also be deleted without consequences.

![Course Lifecycle](./Images/Architecture/Publishing_Process-Course%20Lifecycle.png)

Courses also have an implicit state of being ACTIVE or INACTIVE. This state is not explicit as the states described above. Courses have this state implicitly depending on their start and end-date: A course is ACTIVE, if its start date has passed and its end-date (+ potential offset) has not passed yet. Ideally, only published courses are active. What must be enforced though is that courses cannot be ARCHIVED when they are still active.

## Course Content Lifecycle

Course contents should follow the following lifecycle. When course contents are PUBLISHED or UPDATED, they can be accessed by students.

The UPDATED state enables an indication that a content item has be published, but is now changed. Transitioning to this state should enable to:
* Provide an updated content without deleting/replacing the original content (i.e., both the update and the original should be accessible)
* Provide a reason message for the update (e.g., "In the video, minute 3:45 there was a mistake saying that...")

As all contents belong to exactly one course, their lifecycles cannot be completely isolated: Contents should be archived if and only if their course is archived, and should be deleted whenever their course gets deleted.

UNPUBLISHED contents can also be deleted instantly.

![Countent Lifecycle](./Images/Architecture/Publishing_Process-Content%20Lifecycle.png)
