# Setting up Cypress with Gherkin

1. [Installing the required dependencies](#installing_the_required_dependencies)
   1. [Install Cypress](#install_cypress)
   1. [Install cypress-cucumber-preprocessor](#install_cypress-cucumber-preprocessor)
   1. [Add login hook](#add_login_hook)
      1. [Log in before each test](#log_in_before_each_test)
   1. [Clean up](#clean_up)
1. [Write feature files](#write_feature_files)
1. [Running the tests](#running_the_tests)
1. [Module documentation](#module_documentation)
   1. [cypress](#module_documentation_cypress)
   1. [cypress-cucumber-preprocessor](#module_documentation_cypress-cucumber-preprocessor)

<a name="installing_the_required_dependencies" href=""></a>
## Installing the required dependencies

<a name="install_cypress" href=""></a>
### Install Cypress

Fillow the installation instructions and add the npm scripts:

https://docs.cypress.io/guides/getting-started/installing-cypress.html#Adding-npm-scripts

Also add the `cypress:open` npm script

<a name="install_cypress-cucumber-preprocessor" href=""></a>
### Install cypress-cucumber-preprocessor

Follow the installation instructions:

https://github.com/TheBrainFamily/cypress-cucumber-preprocessor#installation

Make sure to follow the cosmiconfig conventions by adding this to the package.json:

```json
{
    ...
    "cypress-cucumber-preprocessor": {
        "nonGlobalStepDefinitions": true
    },
    ...
}
```

<a name="add_login_hook" href=""></a>
### Add login hook

Create the following file: `/cypress/support/Login.js`.<br />
Import that file in `/cypress/support/index.js`:

```js
import './Login.js'
```

Add the following code to the `Login.js`:

```js
const defaultLoginUrl = 'https://debug.dhis2.org/dev'
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
```js
import { Before } from 'cypress-cucumber-preprocessor/steps'

Before((testCase, callback) => cy.login())
```

<a name="clean_up" href=""></a>
### Clean up

Remove the example files

```
rm -r cypress/integration/examples cypress/fixtures/example.json cypress/support/*
touch cypress/support/index.js
```

<a name="write_feature_files" href=""></a>
## Write feature files

You can now start to write feature files in `/cypress/integration/[Feature_name].js`

<a name="running_the_tests" href=""></a>
## Running the tests

You need to have two environment variables ready when running the tests:
`LOGIN_USERNAME` and `LOGIN_PASSWORD`

There are several options how to pass them to cypress:
https://docs.cypress.io/guides/guides/environment-variables.html#Setting

Just make sure to not add any credentials to git, so if you want to use
the `cypress.env.json` file, add it to your local (global .gitignore; [How to](http://egorsmirnov.me/2015/05/04/global-gitignore-file.html))

<a name="module_documentation" href=""></a>
## Module documentation

<a name="module_documentation_cypress" href=""></a>
### Cypress

https://www.cypress.io/

<a name="module_documentation_cypress-cucumber-preprocessor" href=""></a>
### Cypress Cucumber preprocessor

https://github.com/TheBrainFamily/cypress-cucumber-preprocessor
