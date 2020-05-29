# Testing DHIS 2 applications

At DHIS 2 we've started to test our applications and libraries with e2e tests.
Although time consuming, doing so provides a lot of benifits.
This article will provide a brief overview over the technologies and priciples
we use to test our applications as well as explain why we think they are
important.

The technologies used will be touched briefly and links for further information
are included if you want to dive deeper into the topic

<!-- e2e definition {{{ -->
## What are e2e tests

There are different types of tests. Unit & integration tests test bits and
pieces of your code. And while these are important and give you some security
when working on your code, they do not test the actual application as a whole.
That's where e2e tests come into play. They test the entire product/application
from the beginning to the end, ensuring that the application's flow works as
expected. These tests do not know anything about the underlying code or
architecture and test the application through the user's perspective.
<!-- END: e2e definition }}} -->

<!-- Technologies {{{ -->
## Technologies used at DHIS 2 to write/execute e2e tests

<!-- Technologies :: Cypress {{{ -->
### Cypress

Cypress is a tool with which an application can be tested in a browser. It sets
itself apart from the other, existing e2e technologies by offering a good DX
(developer experience). It's not based on Selenium, has a more modern approach
to handle asynchronous processes, tests are written in JavaScript and has a
very easy to use GUI that simplifies the development of tests significantly.

Tests are executed in the browser, which means that the DOM doesn't need to be
mocked in anyways, it's the real deal!

Cypress has a simple command style structure to select DOM elements and do
assertions. A simple test could look like this:

```js
describe('The user has to login', () => {
  it('should display the login form', () => {
    cy.visit('/')
    cy.get('#login-form').should('exist')
  })
})
```

The code above is a test suite with a single test. The test itself will visit
the homepage and then tries to find the element with the id `login-form` and
the asserts that it exists.

Cypress has a convenient way of dealing with asynchronous processes. There
could be a significant delay between navigating to a page and seeing the
rendered page. The commands that access the DOM have a built-in retry
mechanism. The `get` command retries for 4000 milliseconds. If the element has
not been found by then, the test fails. The timeout values can be overwritten
globally or on a per command basis.
<!-- END: Technologies :: Cypress }}} -->

<!-- START Technologies :: Cucumber {{{ -->
### Cypress plugin: Cucumber Preprocessor

There is a plugin for cypress that enables us to use feature files and write
our tests with the feature file as the instructions for the test code.
The syntax of the feature files is called Gherkin and will be discussed in a
bit.

Feature files have several advantages over writing regular test code. These
files are written in English, so their content is accessible by everyone who
understands English. They serve as specification before the developers work on
a feature / bug, are used as instructions for test code and document the code
just as any other regular test would do.

The official [Gerkin Reference](https://cucumber.io/docs/gherkin/reference/)
contains all necessary information to write proper feature files, this guide
won't go over all the possibilities.

A feature file could look like this:

```feature
Feature: The user should be able to log into the instance in the app

  Scenario: The user visits the app and is not logged in
    Given the user is not logged in
    When the user visits the app
    Then the login form should be displayed

  Scenario: The user visits the app and is logged in
    Given the user is logged in
    When the user visits the app
    Then the login form should not be displayed
    And the home page of the app should be displayed
```

Feature files are used to describe the behavior of the app. In this case,
the title with the `Feature` keyword describes the login feature and the two
`Scenario`s describe possible situations the user might encounter. If the app
ever behaves in an unexpected way, a `Scenario` could be added and tested to
over the bug and its fix in the code base.
<!-- END Technologies :: Cucumber }}} -->

<!-- START Technologies :: d2-utils-cypress {{{ -->
### CLI helper utility

We've written a cli utility (@dhis2/cli-utils-cypress) which handles the
install, run commands and can be used in scripts in the `package.json`.
It wraps both the Cypress and Cucumber-Plugin dependencies, so you don't have
to worry about having compatible versions with our platform.
The `open` and `run` commands both have two arguments:

* `--appStart`
* `--waitOn`

With these two you can control how to start your app and what url to wait for
until cypress starts. This is important as you don't want cypress to start
testing your application before it isn't up and running, here's an example:

```cli
d2-utils-cypress open --appStart "yarn start" --waitOn "http-get://localhost:3000"
```

The values provided to the arguments above are also the default values, so if
they're identical to what your app does, you don't need to supply them.
In case you're wondering about the `http-get` protocol, this is something
special by the `wait-on` npm library. You can read more about this tool on
their [GitHub](https://github.com/jeffbski/wait-on) page.

So by using this utility library, you already reduce the need for 4
dependencies to 1 (`cypress, cypress-cucumber-preprocessor, wait-on,
concurrently` -> `@dhis2/cli-utils-cypress`)
<!-- END Technologies :: d2-utils-cypress }}} -->

<!-- Technologies :: dhis2 custom commands {{{ -->
### Cypress custom commands library

The commands provided by Cypress are quite exhaustive and should allow you to
test virtually anything you can test in the browser. We've added some DHIS 2
specific custom commands that help testing our applications.

We've [decided](https://github.com/dhis2/notes/issues/88) on a naming
convention for the `data-test` attribute. Libraries prefix their `data-test`
attributes with `dhis2-[libname]-` and apps with `dhis2-[appname]-`, e. g.
`dhis2-uicore-button`. But writing out attribute selectors ca be quite
cumbersome and hard to parse when reading the test code, so we've extended the
functionality of the `get` and `find` Cypress commands and added a data-test
attribute selector:

```js
// identical in ui-core
cy.get('{button}')
cy.get('[data-test="dhis2-uicore-button"]')

// identical in the import-export app
cy.get('{idscheme} input')
cy.get('[data-test="dhis2-importexport-idscheme"] input')

cy.get('{idscheme}').find('{button}', { prefix: 'dhis2-uicore' })
cy.get('[data-test="dhis2-importexport-idscheme"]').find('[data-test="dhis2-uicore-button"]')
```

Another useful command is `cy.login()` which will submit the login dialog so
you don't have to worry about that anymore.
<!-- END: Technologies :: dhis2 custom commands }}} -->
<!-- END: Technologies }}} -->

<!-- Hands on {{{ -->
## Creating a small app and add some tests

<!-- Hands on :: Installing {{{ -->
### Installing in a dhis2 platform app

The quickest way to get started is to create a new app with our platform tools,
and some minimal content and test that everything works as expected:

In case don't have our cli tools installed globally, here's how to do it:

```cli
yarn global add @dhis2/cli
```
<!-- END: Hands on :: Installing  }}} -->

<!-- Hands on :: App content {{{ -->
### Adding some rudimentary content

With the above library installed globally, you can run the following commands
in your development directory:


```cli
d2 app scripts init dhis2-testing
cd dhis2-testing
yarn add @dhis2/ui
```

With the commands above, we're creating a new platform app inside a folder
called `dhis2-testing`, navigate into the newly created folder and finally add
the dhis2 ui library as a dependency.

You can find more about creating platform apps on the
[Bootstrapping](https://platform.dhis2.nu/#/bootstrapping) page in the platform
documentation.

In the next step we'll add some content on the home page with simple behavior.
To achieve this, we'll overwrite the contents of the `src/App.js`:

```js
import { Button } from '@dhis2/ui'
import React, { useState } from 'react'

const App = () => {
  const [ showHiddenContent, setShowHiddenContent ] = useState(false)
  const toggleHiddenContent = () => setShowHiddenContent(!showHiddenContent)

  return (
    <div>
      <h1>DHIS 2 Testing app</h1>

      <Button onClick={toggleHiddenContent}>Show hidden content</Button>

      {showHiddenContent && (
        <p>
          This is some hidden content
        </p>
      )}
    </div>
  )
}

export default App
```

Just run `yarn start` inside the `dhis2-testing` folder and have a look what's
being displayed.

The app now displays a button which toggles the visibility of an initially
hidden text.
<!-- END: Hands on :: App content }}} -->

<!-- Hands on :: Cypress structure {{{ -->
### Adding the cypress dependencies & structure

To be able to use cypress and write tests, the dependencies and structure need
to be put in place. This can be done with the d2-utils-cypress library and the
following commands in the root of the app:

```cli
yarn add @dhis2/cli-utils-cypress --dev
d2 utils cypress install
```

The first command will add the cli utitily to the app so we can use the `open`
and `run` commands to execute and develop our tests. The second one will set up
the config files and folder structure that's required for everything to
function.

The `install` command will prompt some questions that have to be answered.
Normally the default values can be used, we'll use the default answers for all
questions, execept for the the backend url, for which we'll use
`https://debug.dhis2.org/dev` so we don't have to set up a local instance.

The output should look like the following:
```
$ d2 utils cypress install
d2-utils-cypress > install 
? URL that Cypress should run tests against: http://localhost:3000
? Glob pattern for the test files to run: **/*.feature
? Record video? No
? The unique Cypress project ID: 
? The DHIS2 instance URL to use as backend: https://debug.dhis2.org/dev
? DHIS2 Username: admin
? DHIS2 Username password: district
Make sure to add `cypress.env.json` to the `.gitignore` file! 
Installing: cypress/plugins/index.js 
Installing: cypress-cucumber-preprocessor.config.js 
Installing: cypress/support/index.js
```

This will create the cypress folder structure required to write tests as well
as some config files like `cypress.json` and `cypress.env.json` so the tests
will use the correct backend and frontend urls.
<!-- END: Hands on :: Cypress structure }}} -->

<!-- Hands on :: Scripts {{{ -->
### Package.json scripts

Before writing the tests, two scripts should be added to the package.json so
the GUI can be opened for development:

```json
{
  // ...
  scripts: {
    // ...
    "cy:open": "d2-utils-cypress open",
    "cy:run": "d2-utils-cypress run"
  }
}
```
<!-- END: Hands on :: Scripts }}} -->

<!-- Hands on :: Feature {{{ -->
### Define the features

Covering the app with tests starts with writing a feature file that describes
the behavior and possible scenarios. In this case the feature is quite simple:
The user can click a button to toggle the visibility of a text. There are two
possible scenarios. Either the text is initially hidden or visible. The feature
file we'll add to the app looks like this:

```feature
Feature: The user can toggle the visibility of a text on the home page

  Scenario: The user shows the text
    Given the text is hidden
    When the user clicks the button
    Then the text should be visible

  Scenario: The user hides the text
    Given the test is visible
    When the user clicks the button
    Then the text should be hidden
```

In our `notes` repository there is a howto article about how to write feature
files, including what grammaticle rules to follow. You can find it
[here](https://github.com/dhis2/notes/blob/master/howto/writing_feature_files.md)
if you want to read more about it.

We'll place the feature file into the `cypress/integration` folder in the root
and call it `home_text_visibility.feature` (final path:
`<root>/cypress/integration/home_text_visibility.feature`). That's the folder
all the feature files and the test code will live in.
<!-- END: Hands on :: Feature }}} -->

<!-- Hands on :: Test code {{{ -->
### Testing the feature file

To test the feature files the test code has to be placed in a folder with the
same name as the feature file. Any JavaScript file inside that folder will be
used. We normally just use `index.js`.

```cli
mkdir cypress/integration/home_text_visibility
touch cypress/integration/home_text_visibility/index.js
```

In the index.js we'll have to import the three step functions before we can
write the actual test code:

```js
import { Given, When, Then } from 'cypress-cucumber-preprocessor/steps'
```

As one steps is shared between the two scenarios, only need to add 5 steps in
that file:

```js
import { Given, When, Then } from 'cypress-cucumber-preprocessor/steps'

Given('the text is hidden', () => {})

Given('the test is visible', () => {})

When('the user clicks the button', () => {})

Then('the text should be visible', () => {})

Then('the text should be hidden', () => {})
```

Now we need to implement the test code for the first `Given` step. It's going
to be entirely from the users perspective, so we'll have to start with
navigating to the homepage. As the text is initially hidden already, we don't
have to actively manipulate the page. If that's the case, it's good practice to
assert that the text is already hidden:


```js
Given('the text is hidden', () => {
  cy.visit('/')
  cy.get('p').should('not.exist')
})
```

The `visit` command will navigate to the home page. Then asserting that the `p`
element does not exist. In the next step the button needs to be clicked:

```js
When('the user clicks the button', () => {
  cy.get('button').click()
})
```

This is simply done by getting the button and then clicking on it with the
built-in `click` function. Finally we need to confirm that the text is visible:

```js
Then('the text should be visible', () => {
  cy.get('p')
    .should('exist')
    .and('be.visible')
})
```
<!-- END: Hands on :: Test code }}} -->

<!-- END: Installing }}} -->
