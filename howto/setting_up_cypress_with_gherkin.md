# Setting up Cypress with Gherkin

## Installing the required dependencies

### Install Cypress

Fillow the installation instructions and add the npm scripts:

https://docs.cypress.io/guides/getting-started/installing-cypress.html#Adding-npm-scripts

Also add the `cypress:open` npm script

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
    const loginAuth = Cypress.env('LOGIN_AUTH')

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

#### Logging in before each test

Add the following shared Cypress `Before` hook: `/cypress/integration/common/login.js`
```js
import { Before } from 'cypress-cucumber-preprocessor/steps'

Before((testCase, callback) => cy.login())
```

## Clean up

Remove the example files

```
rm -r cypress/integration/examples cypress/fixtures/example.json cypress/support/*
touch cypress/support/index.js
```

## Module documentation

### Cypress

https://www.cypress.io/

### Cypress Cucumber preprocessor

https://github.com/TheBrainFamily/cypress-cucumber-preprocessor
