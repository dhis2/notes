# Cypress testing gotchas

### Use cy.should() for assertions to ensure cypress retries them

We were encountering random test failures on CI with our Cypress tests. It turns out that Cypress recommends you to wrap your assertions in `.should` instead of just `.then`:

> Note: Prefer .should() with callback over .then() for assertions as they are automatically rerun until no assertions throw within it but be aware of differences.
> From: https://docs.cypress.io/api/commands/then.html

The differences that you should be aware of are:

> When using a callback function with .should() or .and(), on the other hand, there is special logic to rerun the callback function until no assertions throw within it. You should be careful of side effects in a .should() or .and() callback function that you would not want performed multiple times.
> From: https://docs.cypress.io/api/commands/should.html#Differences

So make sure that there are no side effects triggered in the callback you pass to `.should`. To summarize:

* If you're asserting something, use `.should` instead of `.then` (make sure there are no side-effects)
* If you want to work with the subject yielded from the previous command, and you're not asserting anything, use `.then`

### Leverage Cypress' retry-ability

This relates to the above. An important concept in Cypress is retry-ability. It's Cypress' way of dealing with asynchronicity. A lot of the commands in Cypress will retry until they succeed:

> A core feature of Cypress that assists with testing dynamic web applications is retry-ability. Like a good transmission in a car, it usually works without you noticing it. But understanding how it works will help you write faster tests with fewer run-time surprises.
> ...
> The retry-ability allows the tests to complete each command as soon as the assertion passes, without hard-coding waits. If your application takes a few milliseconds or even seconds to render each DOM element - no big deal, the test does not have to change at all.

Read up on this here: https://docs.cypress.io/guides/core-concepts/retry-ability.html. Note that not all commands automatically retry as that don't always know what constitutes success and failure. This is where appending a `.should` comes in handy, for example: a `.get` that's immediately followed by a `.should` will keep retrying until the `.should` succeeds. Combining commands with assertions means that your test code does not have to know anything about the timing of your app, they'll just wait until the assertions pass.
