# Setting up Cypress with Gherkin

1. [Installing the required dependencies](#installing_the_required_dependencies)
   1. [Install Cypress](#install_cypress)
   1. [Install cypress-cucumber-preprocessor](#install_cypress-cucumber-preprocessor)
   1. [Add login hook](#add_login_hook)
      1. [Log in before each test](#log_in_before_each_test)
   1. [Clean up](#clean_up)
1. [Write feature files](#write_feature_files)
   1. [Example files to test the setup](#example_files)
      1. [Feature file](#example_files_feature)
      1. [Step definitions](#example_files_steps)
      1. [Start app and cypress](#example_files_startup)
1. [Running the tests](#running_the_tests)
1. [Module documentation](#module_documentation)
   1. [cypress](#module_documentation_cypress)
   1. [cypress-cucumber-preprocessor](#module_documentation_cypress-cucumber-preprocessor)

<a name="installing_the_required_dependencies" href=""></a>
## Installing the required dependencies

<a name="install_cypress" href=""></a>
### Install Cypress

* Follow the installation instructions:
https://docs.cypress.io/guides/getting-started/installing-cypress.html
* Also add the `cypress:open` npm script

<a name="install_cypress-cucumber-preprocessor" href=""></a>
### Install cypress-cucumber-preprocessor

Follow the installation instructions:

https://github.com/TheBrainFamily/cypress-cucumber-preprocessor#installation

Make sure to follow the cosmiconfig conventions by adding this to the package.json:

```json
{
    "cypress-cucumber-preprocessor": {
        "nonGlobalStepDefinitions": true
    }
}
```

<a name="add_login_hook" href=""></a>
### Add login hook

In the next step you'll create a `login` method on the `cy` instance by adding
it through the built-in support mechanism.

Create the following file: `/cypress/support/Login.js`.<br />
Import that file in `/cypress/support/index.js`:

```js
import './Login.js'
```

Add the following code to the `Login.js`:

```js
const loginEndPoint = 'dhis-web-commons/security/login.action'

/**
 * This is done through cy.request(...)
 * because Cypress doesn't allow multiple domains per test:
 * https://docs.cypress.io/guides/guides/web-security.html#One-Superdomain-per-Test
 */
Cypress.Commands.add('login', () => {
    const username = Cypress.env('LOGIN_USERNAME')
    const password = Cypress.env('LOGIN_PASSWORD')
    const loginUrl = Cypress.env('LOGIN_URL')
    const loginAuth = `Basic ${btoa(`${username}:${password}`)}`

    return cy
        .request(
            {
                url: `${loginUrl}/${loginEndPoint}`,
                method: 'POST',
                body: {
                    j_username: username,
                    j_password: password,
                    '2fa_code': '',
                },
                headers: { Authorization: loginAuth },
            }
        )
})
```

Check [Running the tests](#running_the_tests) to see how to add the env vars.

<a name="log_in_before_each_test" href=""></a>
#### Log in before each test

Add the following shared Cypress `Before` hook: `/cypress/integration/common/login.js`
It will be executed before each test run automatically because it's in the
`common` directory (this is a `cypress-cucumber-preprocessor` feature).

```js
import { Before } from 'cypress-cucumber-preprocessor/steps'

Before(() => cy.login())
```

<a name="clean_up" href=""></a>
### Clean up

Remove the example files

```
rm -r cypress/integration/examples cypress/fixtures/example.json cypress/support/commands.js
```

And remove the `import './commands.js'` line from `cypress/support/index.js`

<a name="write_feature_files" href=""></a>
## Write feature files

You can now start to write feature files in `/cypress/integration/[Feature_name].js`

<a name="example_files" href=""></a>
### Example files to test the setup

Here are some example files that you can use to test that your setup is
working:

<a name="example_files_feature" href=""></a>
#### Feature file

Put the following into `/cypress/integration/Test.feature`:

```feature
Feature: As a user I want to land on a homepage

  Scenario: User navigates to the index page
    Given the user navigates to the index page
    Then he should be presented a home page
```

<a name="example_files_steps" href=""></a>
#### Step definitions

Put the following into `/cypress/integration/Test/index.js`:

```js
import { Given, Then } from 'cypress-cucumber-preprocessor/steps'

Given('the user navigates to the index page', () => {
  cy.visit(Cypress.env('APP_URL'))
})

Then('he should be presented a home page', () => {
  cy.get('html').should('exist')
})
```

<a name="example_files_startup" href=""></a>
#### Start app and cypress

```sh
# shell 1
yarn start

# shell 2
yarn cypress:open --env LOGIN_USERNAME=[insert user name here],LOGIN_PASSWORD=[insert password here],APP_URL=[insert app url here]
```

The app url will most likely be either `localhost:3000` (CRA apps) or `localhost:8081` (old school apps)

<a name="running_the_tests" href=""></a>
## Running the tests

**You need to have three environment variables ready when running the tests:**
`LOGIN_USERNAME`, `LOGIN_PASSWORD` and `LOGIN_URL`

There are several options how to pass them to cypress:
https://docs.cypress.io/guides/guides/environment-variables.html#Setting

Just make sure to not add any credentials to git, so if you want to use
the `cypress.env.json` file, add it to the `.gitignore`.

There's no defined way of how to create a npm script that will run both `yarn start` and `cypress:open` concurrently,
so as of now you have to run them separately.
There's no need to log in to the backend, it'll be done by cypress and the login support command defined above in this document.

(Note: The reason why there's not a proper concurrent way yet is that `cypress:open` would need to wait for `yarn start` to have finished. But as `yarn start` never exits, there's no way to know that)

<a name="module_documentation" href=""></a>
## Module documentation

<a name="module_documentation_cypress" href=""></a>
### Cypress

https://www.cypress.io/

<a name="module_documentation_cypress-cucumber-preprocessor" href=""></a>
### Cypress Cucumber preprocessor

https://github.com/TheBrainFamily/cypress-cucumber-preprocessor
