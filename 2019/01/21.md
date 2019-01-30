# Summary of Slack discussion 2019/01/21

## Attending

- @mohammer5
- @vilkg
- @varl
- @amcgee
- @jenniferarnesen

## Improve test coverage in our apps

### Lack of tests has consequences (@mohammer5)

* They interrupt the user experience, which can cost you in sales, usage
  metrics, they can even drive customers away permanently.

* Every bug report must be validated by QA or developers.

* Bug fixes are interruptions which cause a costly context switch. Each
  interruption can waste up to 20 minutes per bug, not counting the
  actual fix.

* Bug diagnosis happens outside the normal context of feature
  development, sometimes by different developers who are unfamiliar with
  the code and the surrounding implications of it.

* Opportunity cost: The development team must wait for bug fixes before
  they can continue working on the planned development roadmap.

* The cost of a bug that makes it into production is many times larger
  than the cost of a bug caught by an automated test suite. In other
  words, TDD has an overwhelmingly positive ROI.

**Conclusion**: We agree that a lack of tests is detrimental to the
overall quality and health of our codebases and will strive to improve
the situation incrementally.

### Tests as documentation (@jenniferarnesen)

* Tests help you and other developers understand what your
  component/module/function accomplishes, which is a useful form of
  documentation.

**Conclusion**: Tests adds additional value, for example as a supplement
to documentation. Tests should be designed with equal care as the
functional code as the tests can be read to understand how the module is
supposed to be used in code.

### Test coverage (@amcgee)

* Unit tests are important in some contexts, and we should be obstinate
  about requiring them in those contexts.  Utility functions and non-UI
  libraries are cases where 100% unit test coverage (with jest in our
  case) make a ton of sense.

* I don’t think 100% coverage is useful or practical for
  front-end apps themselves.  There are a lot of grey areas when it
  comes to unit testing react components (without writing contrived
  tests or relying on implementation details), and unless we get that
  very right it becomes a lot of work for developers (both writing tests
  and maintaining them) with minimal gain.

* Other testing tools (like cypress, but definitely not exclusively
  cypress) could help with react component testing but wouldn’t
  necessarily display as 100% line/branch coverage.

* When it comes to testing, I think broad strokes will gain us orders of
  magnitude more improvements to our quality confidence than will fine
  strokes like unit tests (although I agree we should be adding those
  with every PR!)  For instance, end-to-end tests (with and without
  server involvement) can test at high levels that we’re not
  fundamentally breaking functionality anywhere in our complex
  ecosystem.  Similarly, architectural and build process changes (see
  #3) applied to *all* apps in will allow us to leapfrog incremental
  changes in individual apps.

**Conclusion**: We need to define "test expectations" for different
parts of our architecture. Some touched on are functional libs which are
re-used in to a large extent which should be tested to 100%. As the
current state lacks a lot of tests everywhere, we need to start with
broad strokes to improve confidence that our changes are not breaking
subtle parts of the system.

### Application divergence (@amcgee)

* In my view, our fundamental challenge has to do with *divergence*
  across apps, so my proposed solution has been to codify a standard,
  opinionated application architecture which limits the ability of the
  applications to diverge.  The application platform should be shared by
  all apps and should implement a standard
  lint/test/develop/build/ci/stage/deploy pipeline universally.  This is
  what Create React App does if you don’t eject, and I think we should
  use that pattern for DHIS2 apps.

**Conclusion**: Divergence in our applications is killing our ability to
rapidly iterate and will eventually force us into permanent maintenance
mode just to make sure that our applications are up-to-date with our
dependencies. Our applications outnumber devs with a factor of 3-to-1
and the rate of new applications isn't improving the situation. We need
to establish a system of automating our standard application
infrastructure.

Note: work has begun on a [unified CLI for
DHIS2](https://github.com/dhis2/cli). Currently the existing tools we
have are being integrated into this CLI.

### Testability (@vilkg)

* Also, to the testing section I´d like to add consideration of
  testability while coding new features: i.e adding meaningful selectors
  (id, data-test-id or any other). This will not only benefit us when
  creating e2e tests, but also help organisations like PEPFAR with
  stability of their own test suites. 
  Selectors should be meaningful and unique (at least on app or page). 

  Agreed on using data-test-id and stripping those in prod if needed.

  https://www.npmjs.com/package/babel-plugin-jsx-remove-data-test-id. 

**Conclusion**: When writing E2E tests using Cypress we will add these
`test-data-id` attributes anyway, but to help with the general E2E tests
we should start to add these attributes in preparation as well.
