# Testing
"Software testers succeed where others fail." – Anonymous

## Testing strategy
### How do we test?
- Classical
- Test driven
- Test first

**Suggestion:** Since we do not have an explicit requirements base I would recommend using a **test first** approach. Therefore our test specification is basically an implicit documentation of our requirements.

### Test levels
- Unit testing
- Integration testing
- System testing
- Acceptance testing

### Test methods
- Smoke tests
- Performance tests
- Fuzzy tests
- Equivalence class testing
- Requirements based
- Regression tests
- Black-/White/Grey-Box testing

### Issue tracking?
Feedback loop in Jira? Bugtracker
### Metrics?
Code coverage?
Visualization? Tracking? -> Grafana?
[Pro Tips: Using Grafana in Quality Assurance](https://grafana.com/blog/2018/11/29/pro-tips-using-grafana-in-quality-assurance/)

What do we want to achieve?
- code coverage 100%
- pass rate?
- "optional" tests?

### Test automatisation?
What do we test when, how and where?
local, Jenkins stages...
## Test tools:
### Frontend
Expo recommends **Jest** as "most widely used JavaScript unit testing framework"
<br>
[Expo with Jest](https://docs.expo.io/guides/testing-with-jest/)

### Backend
JHipster does a lot of stuff:
[JHipster tests](https://www.jhipster.tech/running-tests/)
- **Unit tests** using **JUnit 5**
- **Integration tests** using the **Spring Test Context framework**
- **UI tests** with **Jest**
- **Architecture tests** with **ArchUnit**

Optionally, JHipster can also generates:
- **Performance tests** with **Gatling**.
- **Behaviour-driven tests** with **Cucumber**.
- **Angular/React/Vue integration tests** with **Protractor**.

## Further readings
[GeeksforGeeks - Software Testing Strategies](https://www.geeksforgeeks.org/software-testing-strategies/)
<br>
[browserstack - Software Testing Strategies and Approaches](https://www.browserstack.com/guide/software-testing-strategies-and-approaches)
<br>
[Wikipedia - Test strategy](https://en.wikipedia.org/wiki/Test_strategy)
<br>
[Wikipedia - Software testing](https://en.wikipedia.org/wiki/Software_testing)
<br>
[Wikipedia - Test-driven development](https://en.wikipedia.org/wiki/Test-driven_development)
<br>
[TDD vs Test first](https://refactoring-legacy-code.net/tdd-vs-test-first/)
<br>
[Test Strategy for Microservices](https://www.gocd.org/2018/05/08/continuous-delivery-microservices-test-strategy/)
<br>
[Microservices Testing Strategies, Types & Tools: A Complete Guide](https://www.simform.com/microservice-testing-strategies/)

