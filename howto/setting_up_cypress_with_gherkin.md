# Setting up Cypress with Gherkin

1. [Installing the required dependencies](#installing_the_required_dependencies)
   1. [Install Cypress](#install_cypress)
   1. [Install cypress-cucumber-preprocessor](#install_cypress-cucumber-preprocessor)
   1. [Install concurrently and wait-on](#install_concurrently_and_wait-on)
   1. [Add env var setup script](#add_env_var_setup_script)
   1. [Add scripts to package.json](#add_scripts_to_package-json)
   1. [Add login hook](#add_login_hook)
      1. [Log in before each test](#log_in_before_each_test)
   1. [Clean up](#clean_up)
1. [Write feature files](#write_feature_files)
   1. [Example files to test the setup](#example_files)
      1. [Feature file](#example_files_feature)
      1. [Step definitions](#example_files_steps)
      1. [Start app and cypress](#example_files_startup)
      1. [Add environment variables](#example_files_env_vars)
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

Then run `yarn cypress:open` to generate the directories and example files.

<a name="install_cypress-cucumber-preprocessor" href=""></a>
### Install cypress-cucumber-preprocessor

Follow the installation **and "Cypress Configuration"** instructions:

https://github.com/TheBrainFamily/cypress-cucumber-preprocessor#installation

Make sure to follow the cosmiconfig conventions by adding this to the **package.json**:

```json
{
    "cypress-cucumber-preprocessor": {
        "nonGlobalStepDefinitions": true
    }
}
```

<a name="install_concurrently_and_wait-on" href=""></a>
### Install concurrently and wait-on

Run the following:

```
yarn add -D concurrently wait-on
```

<a name="add_env_var_setup_script" href=""></a>
### Add env var setup script

Create a `scripts` folder in the root of your project and add
`scripts/check_env_vars.js` with the following contents:

```js
const fs = require('fs')
const path = require('path')
const readline = require('readline')

const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout,
})

const read = (...args) =>
    new Promise(resolve => {
        rl.question(...args, resolve)
    })

const DEFAULT_ENV_FILE_PATH = path.join(__dirname, '../', 'cypress.env.json')

const REQUIRED_ENV_VARS = {
    LOGIN_USERNAME: '',
    LOGIN_PASSWORD: '',
    APP_URL: 'localhost:3000',
}

const getExistingEnvVars = envFilePath => {
    const fileContents = fs.readFileSync(envFilePath, { enconding: 'utf8' })
    let envVars = {}

    try {
        envVars = JSON.parse(fileContents)
    } catch (e) {
        console.error("Couldn't parse cypress.env.json")
        console.error(e.message)
        process.exit(1)
    }

    return envVars
}

const requestInformationForEnvVar = ({ resolve, defaultValue, envVar }) => {
    read(`Please provide the value for ${envVar}${defaultValue}\n`).then(
        answer => {
            if (answer === '' && REQUIRED_ENV_VARS[envVar]) {
                resolve([envVar, REQUIRED_ENV_VARS[envVar]])
            } else if (answer !== '') {
                resolve([envVar, answer])
            } else {
                requestInformationForEnvVar({ resolve, defaultValue, envVar })
            }
        }
    )
}

const requestMissingInformation = missingEnvVars => {
    return missingEnvVars.reduce((process, envVar) => {
        return process.then(answers => {
            const defaultValue = REQUIRED_ENV_VARS[envVar]
                ? ` (${REQUIRED_ENV_VARS[envVar]})`
                : ''

            return new Promise(resolve => {
                const customResolve = answer => resolve([...answers, answer])
                requestInformationForEnvVar({
                    resolve: customResolve,
                    defaultValue,
                    envVar,
                })
            })
        })
    }, Promise.resolve([]))
}

const writeMissingInformation = ({
    existingEnvVars,
    answerRequests,
    envFilePath,
}) => {
    return answerRequests.then(answers => {
        const valuesObject = answers.reduce(
            (curValuesObject, [envVar, value]) => ({
                ...curValuesObject,
                [envVar]: value,
            }),
            existingEnvVars
        )

        fs.writeFileSync(envFilePath, JSON.stringify(valuesObject, null, 4))

        return valuesObject
    })
}

const addMissingEnvVars = envFilePath => {
    const existingEnvVars = getExistingEnvVars(envFilePath)
    const missingEnvVars = Object.keys(REQUIRED_ENV_VARS).filter(
        envVar => !(envVar in existingEnvVars)
    )
    const answerRequests = requestMissingInformation(missingEnvVars)

    return writeMissingInformation({
        existingEnvVars,
        answerRequests,
        envFilePath,
    })
}

const createEnvFile = envFilePath => {
    const missingEnvVars = Object.keys(REQUIRED_ENV_VARS)
    const answerRequests = requestMissingInformation(missingEnvVars)

    return writeMissingInformation({
        existingEnvVars: {},
        answerRequests,
        envFilePath,
    })
}

const checkEnvFile = () => {
    const envFilePath = DEFAULT_ENV_FILE_PATH

    const job = !fs.existsSync(envFilePath)
        ? createEnvFile(envFilePath)
        : addMissingEnvVars(envFilePath)

    return job.then(() => rl.close())
}

checkEnvFile()
    .then(() => exit(0))
    .catch(() => exit(1))
```

<a name="add_scripts_to_package-json" href=""></a>
### Add scripts to package.json

Add the following scripts.
They will allow you to run/open cypress with just one command

```
"cypress:start": "BROWSER=none yarn start",
"cypress:envtest": "node ./scripts/check_env_vars.js",
"cypress:browser": "cypress open --config baseUrl=http://localhost:3000,defaultCommandTimeout=15000",
"cypress:ci": "NO_COLOR=1 cypress run -b $BROWSER --config baseUrl=http://localhost:3000,defaultCommandTimeout=15000",
"cypress:open": "yarn cypress:envtest && concurrently --kill-others -n cra,cypress 'yarn cypress:start' 'wait-on http-get://localhost:3000 && yarn cypress:browser --env LOGIN_URL=$REACT_APP_DHIS2_BASE_URL'",
"cypress:run": "yarn cypress:envtest && concurrently --kill-others --success first -n cra,cypress 'yarn cypress:start' 'wait-on http-get://localhost:3000 && yarn cypress:ci --env LOGIN_URL=$REACT_APP_DHIS2_BASE_URL'"

```

<a name="add_login_hook" href=""></a>
### Add login hook

In the next step you'll create a `login` method on the `cy` instance by adding
it through the built-in support mechanism.

Create the following file: `/cypress/support/Login.js`.<br />

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

Import that file in `/cypress/support/index.js`:

```js
import './Login.js'
```

Check [Add environment variables](#example_files_env_vars) to see how to add the env vars.

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

<a name="example_files_env_vars" href=""></a>
#### Add environment variables

**You need to have four environment variables ready when running the tests:**
`LOGIN_USERNAME`, `LOGIN_PASSWORD`, `LOGIN_URL` and `APP_URL`

* `LOGIN_USERNAME` and `LOGIN_PASSWORD` are what you'd enter on a dhis2
instance's login page
* `LOGIN_URL` is the domain (and suffix, e. g. `/dev` or `/2.31.5`) of your
  dhis2 instance's login page
* `APP_URL` is the url of your local development app

There are several options how to pass them to cypress:
https://docs.cypress.io/guides/guides/environment-variables.html#Setting

Just make sure to not add any credentials to git, so if you want to use
the `cypress.env.json` file, add it to the `.gitignore`.

<a name="example_files_startup" href=""></a>
#### Start app and cypress

```sh
# shell 1; Make sure to use the correct backend (same as "LOGIN_URL")
yarn start

# shell 2
yarn cypress:open --env LOGIN_USERNAME=[insert user name here],LOGIN_PASSWORD=[insert password here],APP_URL=[insert app url here]
```

The app url will most likely be either `localhost:3000` (CRA apps) or `localhost:8081` (old school apps)

<a name="running_the_tests" href=""></a>
## Running the tests

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
