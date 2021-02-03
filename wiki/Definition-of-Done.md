The Definition of Done is a collection of criteria that need to be fulfilled before an issue is considered as "Done".
Our idea is, to have a review process at the end of each ticket, where following criteria hold.
After they are fulfilled, the issue in Jira can be moved from "Review" to "Done"
This helps us to ensure a higher quality.

<br>

# Criteria:

- Tests are green
  - Code passes automatic tests (JUnit/Jest)
  - User Tests were done on local system for the implemented features
- Style is ok
  - Code adheres to Styleguide
  - No dead code
  - No unnecessary comments
- Code is pushed to 'dev'
- Acceptance criteria are fulfilled
- Documentation (Wiki/JavaDoc is written)
- Frontend-specific implementation was considered
  - Language support for "en" and "de"
  - Support web, android, ios

<br>
<br>

---

If there are certain criteria that can't be fulfilled because they are not in the ticket's nature, they can be ignored.
One example would be an issue where the goal is to write documentation. There, you do not need to check for dead code, but should push it to master, before declaring the issue as "done".
