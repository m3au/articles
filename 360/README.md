<h1 align="center">Welcome to Play - Xempus e2e Automation Framework 📦🐈</h1>

> Typescript API and UI Testing Engine based on Microsoft Playwright and Playwright Test Runner,
> sugar coated with BDD and HTML/Junit reports.

![Framework illustration](docs/framework.webp?raw=true 'Playwright Playwright')

This is a Keyword-driver / BDD implementation of Playwright Test runner framework
using custom Typescript components and fixtures.
The play CLI (engine) is built with yargs to allows custom args for command execution.

For more documentation on Playwright, please visit [playwright.dev](https://playwright.dev/) and [yargs](http://yargs.js.org/).

---

**Table of Contents:**

- [Requirements and installation](#requirements-and-installation)
  - [How to setup playwright project](#how-to-setup-playwright-project)
    - [via docker](#via-docker)
    - [or locally](#or-locally)
  - [vscode (strongly recommend)](#vscode-strongly-recommend)
  - [node.js](#nodejs)
  - [Installing the project and all dependencies](#installing-the-project-and-all-dependencies)
- [Project and folder structure](#project-and-folder-structure)
  - [Playwright settings](#playwright-settings)
  - [Components](#components)
  - [Fixtures](#fixtures)
  - [Test Data](#test-data)
  - [Gherkin](#gherkin)
  - [Tests](#tests)
  - [Scripts](#scripts)
    - [Contract Generator](#contract-generator)
  - [Reports](#reports)
- [Test Execution](#test-execution)
  - [Test Runner Overview](#test-runner-overview)
  - [Different ways of Test Execution](#different-ways-of-test-execution)
  - [Test Execution Report](#test-execution-report)
  - [Additional Commands](#additional-commands)
  - [CI/CD pipelines and Quality gates](#cicd-pipelines-and-quality-gates)
  - [Microsoft Playwright VS Code Plugin](#microsoft-playwright-vs-code-plugin)
- [Configurations](#configurations)
  - [Node settings](#node-settings)
  - [Git settings](#git-settings)
  - [Typescript settings](#typescript-settings)
  - [ESLint settings](#eslint-settings)
  - [Gherkin settings](#gherkin-settings)
  - [Prettier settings](#prettier-settings)
  - [IDE settings](#ide-settings)
- [Dependencies](#dependencies)
  - [NPM Dependencies](#npm-dependencies)
  - [npm-check-updates](#npm-check-updates)
- [Contributing](#contributing)
  - [Codebase ownership](#codebase-ownership)
  - [Trunk based development](#trunk-based-development)
  - [Pair programming](#pair-programming)
    - [Continuous Review](#continuous-review)
- [Learning and References](#learning-and-references)

---

# Requirements and installation

## How to setup playwright project

There is two ways to run the test test.

### via docker

```sh
git clone ssh://git@bitbucket.xempus.io/plat/playwright.git
cd playwright
bin/run
bin/report
open http://0.0.0.0:9323 # in a separate terminal open this URL
```

To run different test inside the docker, adjust the [run script](./bin/run)

### or locally

```sh
git clone ssh://git@bitbucket.xempus.io/plat/playwright.git # clone
cd playwright
nvm install
nvm use
npm install
npm run setupValidationCheck
npm run report
```

We suggest running the test locally as it provides increased flexibility to leverage Playwright extensions within VS Code, offering an enhanced and more seamless testing experience.

## vscode (strongly recommend)

The project contains workspace settings and recommended plugins and extensions that only work on
[VS Code](https://code.visualstudio.com/), so we **strongly recommend** the adoption of the IDE.

To setup your VSCode

- install all recommended [VSCode extensions](.vscode/extensions.json)
- Change Typescript to use the [workspace version](.vscode/settings.json)

## node.js

This project runs on Node.js. In case you're using `node` at different projects with different versions. This will pickup the correct version from the
`.nvmrc` file.

We recommend installing node through [nvm](https://github.com/nvm-sh/nvm)
so that you can switch versions on demand, for more information check
[Installing nvm](https://www.google.com/search?q=installing+nvm).

```sh
nvm install
```

It usually automatically switches to the new version, but you might need to:

```sh
nvm use
```

## Installing the node modules and all dependencies

You can run the following command on the root folder to install all the dependencies:

```sh
npm install
```

This will also automatically run the `postinstall` script listed under the **scripts** section of
the [package.json](./package.json) file.

If everything is in place, you can now run tests, try `npm run setupValidationCheck` to run a single test.

---

# Project and folder structure

## Playwright settings

All the playwright settings are located in the [playwright.config.ts](./playwright.config.ts) file.
We do have some custom setting for specific projects that can be found inside the folder [test-suites](./test-suites)

Most settings can be overridden by environment variables, so that we can have different settings just by using the CLI.
For example, if you want to run the tests on a different browser, you can do it by running:

```sh
browserName=chromium npm run
```

For a complete list of settings, check the [Playwright documentation](https://playwright.dev/docs/test-configuration).

## Components

## Fixtures

## Test Data

We decoupled the test data from the tests, so that we can reuse the same tests with different data.
Each test usually has a test file (.test.ts), a Gherkin file (.feature) and a data file (.data.ts).
Test data files are usually structured to match the test file and Feature file by Scenario.
E. g. the test file `activation.test.ts` has a data file `activation.data.ts` and the Feature file `activation.feature`.
If you take the following example:

```gherkin
Feature: Activation
  As an Advisor, I want to be able to activate my registered new user

  Background:
    Given I have registered a new user
    And I have received an activation email

  Scenario: 1 Activate User
    When I open the Activate Account link in the email
    And I agree to Terms and conditions
    And I provide my password
    And I provide my Insurer
    And I provide my Agent number
    And I open the Agent Area link
    Then I see the Home page

  Scenario: 2 Open Activation link of an activated User
    When I open the Activate Account link in the email
    Then I see the Home page

```

The data file will look like this:

```typescript
// The exported data object is an array of objects, each object corresponds to a Scenario in the Feature file
const data = new Gherkin(__filename, [
  {}, // <-- this data object corresponds to the Background of the Feature File (or the BeforeEach on the tests)
  // The code below corresponds to the First Scenario of the Feature file (and the first test on the test file)
  {
    integration: { manager: { user: agent('agent') } }, // Each object has a key that corresponds to the environment
    hotfix: {
      // Each environment has a key that corresponds to the Whitelabel
      manager: { user: agent('agent') },
    },
    alpha: {
      manager: {
        // Inside the whitelabel we have a key that corresponds to the actual data used in the test
        user: agent('agent'),
      },
    },
  },
  // The code below corresponds to the Second Scenario of the Feature file (and the second test on the test file)
  {
    integration: { manager: { user: agent('agent') } },
    hotfix: {
      manager: {
        user: [
          // It could also be an array of data objects, in case we need additional data for the same test
          agent('agent'),
          agent('multi-agent'),
        ],
      },
    },
    alpha: { manager: { user: agent('agent') } },
  },
])
```

## Gherkin

We use Gherkin to write the rationale of the tests, and to make them more readable and understandable.
More information regarding the use of this language can be found in <https://confluence.xempus.com/x/iJZxCw>.
For the time being we are not using the Gherkin the "Cucumber way" where there is a step definition file, as we chose to
implement the steps directly in the test files themselves (or actually in the components methods, following a Page Object Model architecture),
so that we can have a better control of the tests.

This means that the only really important part of the Gherkin file is the Feature name, and the Scenario names.
All the other parts of the Gherkin file are just for documentation purposes.

This also means that Examples, Scenario Outlines, and Backgrounds are not used in our tests.

## Tests

The tests are located in the `tests` folder, and are organized by Actor ("agent, employer, employee...").
All tests should be written using the [Playwright](https://playwright.dev/) framework.

The test files structure is as follows:

```typescript
import { test } from 'app/test' // Basic import of the custom test implementation
// The customized test implementation is a wrapper of the Playwright test framework with some extra features

import data from './authentication.data' // This is where we import the test data file to use in the tests

test.use({ data }) // This is where we pass the test data to the test framework

const { name, children } = data.gherkin.feature

// The test Describe name (block of tests) is taken from the Feature name in the Gherkin file
test.describe(name, async () => {
  // In this case it would be "Authentication"
  test.beforeEach(async ({ page, apps }) => {
    await advisor.login.goto()
  })

  // The test name itself is taken from the Scenario name in the Gherkin file
  test(children[1].scenario.name, async ({ apps, user }) => {
    await advisor.login.submitLoginForm(user)
    await advisor.home.isVisible()
  })

  test(children[2].scenario.name, async ({ apps, user }) => {
    // we use 2 fixtures usually, the apps and the user
    // The apps fixture is a collection of all the apps that we have in the project
    // The user fixture is the data objects that we pass to the test data file
    await advisor.login.submitLoginForm(user)
    await advisor.login.hasInvalidCredentialsErrorMessage()
  })
})
```

## Scripts

### Contract Generator

This script enables to create, delete, deactivate contract that follows BiPro and RNext standard and not csv import.

Please find the commands as below,

To create a contract:

```bash
COMPANY_IDENTIFIER=XXXX-XXXX npm run contract -- --grep=create
```

To delete a contract:

```bash
CONTRACT_NUMBER=${CONTRACT_NUMBER} npm run contract -- --grep=delete
```

To deactivate a contract (applicable only for RNext import):

```bash
CONTRACT_NUMBER=${CONTRACT_NUMBER} npm run contract -- --grep=deactivate
```

For the other possible CLI Variables that could be used to create contract, please refer to contract.base.ts file inside the [bipro](./scripts/contract-generator/bipro) and [rnext](./scripts/contract-generator/rnext) folders

## Reports

Playwright has a built-in reporting system that can be used to generate reports from the test results.
The reports are generated in the `reports` folder, based on the data available inside the `test-results` folder.
This folder is created during test executions, and contains all the test results from the last execution,
by the Test Runner.

The reports also contain the Stack traces generated by the Test Runner, and are later uploaded into the
HTML Report that is Published by Jenkins at the end of the execution.
The HTML Report is the go-to report for our implementation, but Playwright also has some other built-in reports.
You can find more information about them in the [Playwright Reports](https://playwright.dev/docs/test-reporters).

On the Jenkins execution, the HTML Report is published through a Post-Build Action, and the report is available here:

![Jenkins HTML Test Report](docs/jenkins_report.png?raw=true 'Playwright Test Report')

# Test Execution

## Test Runner Overview

The Playwright test runner, while resembling the Mocha test runner in some aspects, offers additional features enhancing its power and usability. Detailed information on the test runner can be found in the [Playwright Test Runner](https://playwright.dev/docs/intro#running-the-example-test).

All generated data is stored in the `test-results` folder. This folder is created during test executions.

## Different ways of Test Execution

### General Test Execution

To execute all tests, simply enter the following command:

```sh
npm run test
```

### Running Tests by Scope

You can run tests based on their scope using the following commands:

```sh
npm run smoke
npm run sanity
npm run onpush
npm run regression
npm run platform
```

### Running Tests by Scope and Key Actors

To run the tests based on the scope and key actors (Agent/Advisor, Employer/Manager, Employee/Consumer):

```sh
npm run regression tests/Agent tests/Employer
```

### Running Specific Tests using grep command

To run a specific test, utilize the grep option. You can specify either the Feature name or Scenario names directly within the Gherkin files:

```sh
npm run regression -- --grep="1 Roundtrip"
```

E.g.: --grep="@smoke" or --grep="1 Activation"

```gherkin
Feature: 1 Activation @smoke

  Scenario: 1 Roundtrip
    Given I am logged in as "employee"
    When I go to "roundtrip"s
    Then I should see "roundtrip"
```

You can also specify which tests you want to run using Mocha's **test.only() / test.skip()** strategies inside the tests

### Running Specific Tests using CLI variables

The following CLI variables are used by the tests: what you can change via command lines.

- ENVIRONMENT,
- WHITELABEL,
- quiet,
- forbidOnly,
- fullyParallel,
- globalTimeout,
- timeout,
- maxFailures,
- repeatEach,
- retries,
- workers,
- expectTimeout,
- headless,
- navigationTimeout,
- actionTimeout,
- browserName,
- slowMo,
- locale,
- trace,
- video,

You can have your local CLI variables in a file called `.env` in the root folder of the project (Copy the .env.template file and rename/modify it).

For example, using the following command on the terminal:

```sh
# custom argv "CLI variables"
ENVIRONMENT='alpha' video='on' npm run regression
```

To find out more about the available commands, check the [Playwright CLI commands](https://playwright.dev/docs/test-cli).

## Test Execution Report

- `npm run report` runs the Report server with default settings, usually on <http://127.0.0.1:9323/>
  and opens the Browser page. Refresh the page after a test run to see the latest results of the execution.

### Additional Commands

In the `package.json` file, we have defined several commands that execute specific scripts along with their corresponding configurations. These commands are set up to simplify the execution process, providing a convenient way to run various tasks.

## CI/CD pipelines and Quality gates

All Playwright project related Jenkins jobs can be found here: <https://jenkins.xempus.io/job/platform/job/playwright/>. All the setting for those jobs are located inside the folder [jenkins](./jenkins).

The workflow for quality gate and deployment can be referred to [Quality Gate Management for Deploy Pipeline](./jenkins/quality-gates/README.md).

## Microsoft Playwright VS Code Plugin

You can also run and interact with the **\*.test.ts** files in the project with a special Panel that only
appears after you install the extension [Microsoft - Playwright Test for VSCode](https://marketplace.visualstudio.com/items?itemName=ms-playwright.playwright).

![Framework illustration](docs/vscode_extension.png?raw=true 'Microsoft Playwright VSCode Extension'){height=400px}

---

# Configurations

The project has several configuration files:

## Node settings

This project enforces the use of npm by setting 'engine-strict=true' on the file [.npmrc](./.npmrc) and [.nvmrc](./.nvmrc)
at the root folder.

## Git settings

The file [.gitattributes](./.gitattributes) at the root folder enforces rules like Encoding (UTF-8) and
End-of-Line (CR/CRLF) across all files in the repo.
[.gitignore](./.gitignore) you already know.

## Typescript settings

The typescript configuration can be found at the root folder [tsconfig.json](./tsconfig.json) file, together
with the typings that are automatically picked up by the IDE inside the file [Advisor Types](./components/advisor/types.d.ts), [Manager Types](./components/manager/types.d.ts).

## ESLint settings

The linting of the .ts files for Typescript issues and Playwright issues is done using ESLint, and you can
find the settings in the eslintConfig section of [package.json](./package.json). You can learn more about ESLint at
[eslint.org](https://eslint.org/) and also at [eslint-plugin-playwright](https://www.npmjs.com/package/eslint-plugin-playwright).

## Gherkin settings

To lint and Autoformat the .feature files the project depends on the VS Code extension [Cucumber (Gherkin)
Full Support](https://marketplace.visualstudio.com/items?itemName=alexkrechik.cucumberautocomplete).

The settings for this plugin are located in the file [.gherkin-lintrc](./.gherkin-lintrc.json) in the root folder
and the IDE binding is done in the workspace settings file [./.vscode/settings.json](./.vscode/settings.json).

```json
"[feature]": {
  "editor.defaultFormatter": "alexkrechik.cucumberautocomplete"
},
```

## Prettier settings

The Code style is also fixed by a VS Code plugin, [Prettier - Code formatter](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode),
together with the workspace settings found at [./.vscode/settings.json](./.vscode/settings.json) listed below:

```json
"editor.defaultFormatter": "esbenp.prettier-vscode",
"editor.formatOnSave": true,
"editor.formatOnPaste": false,
```

## IDE settings

Besides the settings mentioned above, the project also has a <u>Dictionary</u>, also inside the file [./.vscode/settings.json](./.vscode/settings.json),
so that the plugin [Code Spell Checker](https://marketplace.visualstudio.com/items?itemName=streetsidesoftware.code-spell-checker)
can ignore strange words; also the German language extension is enabled.

The IDE should pickup on the settings file [.editorconfig](./.editorconfig) for indentation, and other rules
while you are typing or creating new files.

The project is also configured to allow the use of comments in json files.

We prepared a list of <u>**Recommended Extensions**</u> to make your development more wholesome 🦄, if you
open VS Code on the root folder of the project, it should automatically suggest you to install all of them.

[./.vscode/extensions.json](./.vscode/extensions.json)

```json
  "recommendations": [
    "dbaeumer.vscode-eslint",
    "streetsidesoftware.code-spell-checker",
    "streetsidesoftware.code-spell-checker-german",
    "vscode-icons-team.vscode-icons",
    "pflannery.vscode-versionlens",
    "eg2.vscode-npm-script",
    "esbenp.prettier-vscode",
    "ms-playwright.playwright",
    "ryanrosello-og.playwright-vscode-trace-viewer",
    "editorconfig.editorconfig",
    "muralidharan92.cuke-step-definition-generator",
    "alexkrechik.cucumberautocomplete",
    "rbbit.typescript-hero",
    "amatiasq.sort-imports",
    "wayou.vscode-todo-highlight"
  ]
```

---

# Dependencies

## NPM Dependencies

- [@playwright/test](https://ghub.io/@playwright/test): Playwright test runner
- [@types/chance](https://ghub.io/@types/chance): TypeScript definitions for chance
- [@types/dotenv-parse-variables](https://ghub.io/@types/dotenv-parse-variables): TypeScript definitions for dotenv-parse-variables
- [@types/luxon](https://ghub.io/@types/luxon): TypeScript definitions for luxon
- [@types/node](https://ghub.io/@types/node): TypeScript definitions for Node.js
- [@types/properties-reader](https://ghub.io/@types/properties-reader): TypeScript definitions for properties-reader
- [@typescript-eslint/eslint-plugin](https://ghub.io/@typescript-eslint/eslint-plugin): TypeScript ESLint rules
- [@typescript-eslint/parser](https://ghub.io/@typescript-eslint/parser): An ESLint parser which leverages TypeScript ESTree to allow for ESLint to lint TypeScript source code.
- [chalk](https://ghub.io/chalk): Terminal string styling done right
- [chance](https://ghub.io/chance): Random generator helper for JavaScript
- [console-table-printer](https://ghub.io/console-table-printer): Print tables in console with ease. Support grouping, aggregation, filtering, styling, border and more.
- [csv](https://ghub.io/csv): Full featured CSV parser with simple api and tested against large datasets.
- [date-fns](https://ghub.io/date-fns): Modern JavaScript date utility library
- [delete-empty](https://ghub.io/delete-empty): Delete empty folders and empty files (recursively)
- [dotenv](https://ghub.io/dotenv): Loads environment variables from .env file
- [dotenv-parse-variables](https://ghub.io/dotenv-parse-variables): Parse environment variables from .env files and apply them to process.env
- [eslint](https://ghub.io/eslint): An AST-based pattern checker for JavaScript.
- [eslint-config-prettier](https://ghub.io/eslint-config-prettier): Turns off all rules that are unnecessary or might conflict with Prettier.
- [eslint-plugin-markdown](https://ghub.io/eslint-plugin-markdown): ESLint plugin for Markdown code blocks.
- [eslint-plugin-playwright](https://ghub.io/eslint-plugin-playwright): ESLint plugin for Playwright test runner.
- [eslint-plugin-prettier](https://ghub.io/eslint-plugin-prettier): Runs prettier as an eslint rule.
- [gherkin-parse](https://ghub.io/gherkin-parse): A Gherkin parser that generates an AST (Abstract Syntax Tree) from Gherkin feature files.
- [luxon](https://ghub.io/luxon): A library for working with dates and times in JS
- [path](https://nodejs.org/api/path.html#path_path_join_paths): Node.JS path module.
- [prettier](https://ghub.io/prettier): Prettier is an opinionated code formatter.
- [properties-reader](https://ghub.io/properties-reader): Read and parse Java .properties files in node.js.
  Supports single-line and multi-line strings, comments beginning with # or !, and values spanned across multiple lines. Does not support Unicode escapes.
- [typescript](https://ghub.io/typescript): TypeScript is a language for application scale JavaScript development
- [url](https://nodejs.org/api/url.html#url_url_parse_urlstring_parsequerystring_slashesdenotehost): Node.JS url module.

## npm-check-updates

We created a script that checks for outdated dependencies and updates them, directly on the package.json file.
Just run `npm run bump` to update the dependencies. For further details refer [HowToBumpDependencies](https://confluence.xempus.com/display/EN/How+to+bump+dependencies+for+Playwright)

---

# Contributing

To contribute to this project, please follow the guidelines found in <https://confluence.xempus.com/display/EN/Contributing+to+the+codebase>
Please also read the Contribution Guidelines in the [CONTRIBUTION_POLICY.md](CONTRIBUTION_POLICY.md) file.

## Codebase ownership

Everyone owns the `components` folder, as it hosts the methods that are used by the tests.
But usually the `tests` folder is owned by the team that owns the **actor** that is being tested.
You can find more information about ownership in the [CODEOWNERS.md](CODEOWNERS.md) file.

## Trunk based development

In the trunk-based development model, all developers merge small, frequent updates to a core **trunk** branch
with open access to it. Often it is simply the **main** branch.

Why CI and not branching

- [Continuous Integration vs Feature Branch Workflow](https://www.youtube.com/watch?v=v4Ijkq6Myfc)
- [Why CI is BETTER Than Feature Branching](https://www.youtube.com/watch?v=lXQEi1O5IOI)

How to do it

**Commit messages**
Commit messages matter. Here's how to write them well

- A properly formed git commit subject line should always be able to complete the following sentence
  _If applied, this commit will `<your subject line here>`_
  For example: When we have added tests for authentication feature, the commit message could be:
  _`Add tests for authentication`_

- Write your commit message in the imperative mode: _"Fix bug"_ and **not** _"Fixed
  bug"_ or _"Fixes bug"_. This convention matches up with commit messages
  generated by commands like git merge and git revert.

- Capitalize the subject line: _"Implement login feature"_ and not _"implement login feature"_.

## Pair programming

### Continuous Review

Pair programming is becoming code review more and more in the industry.

So we should have pair programming - 2 people vs. the whole team - 10+ people, and we expect a lot of comments.
This is not only about bugs, this is about architecture, simplicity, and readability. To do code review after merge
to some kind of trunk / main branch is a huge waste. What if someone spots a bug at that point?
Feature has to go back to development, team has to switch context fast, because production code is broken and current
work is interrupted, which probably leads to unstable sprints.

# Learning and References

We found the following literature to be helpful:

- Video about Playwright [Playwright: A New Test Automation Framework for the Modern Web [Webinar Recording]](https://www.youtube.com/watch?v=_Jla6DyuEu4)
- Video on how to use it [Playwright Masterclass - Playwright Test](https://www.youtube.com/watch?v=VKvZSpSWDZw)
- Playwright documentation [https://playwright.dev/](https://playwright.dev/)
- Yargs documentation [https://yargs.js.org/docs/](https://yargs.js.org/docs/)
- Prettier documentation [https://prettier.io/docs/en/index.html](https://prettier.io/docs/en/index.html)
- ESLint documentation [https://eslint.org/docs/latest/](https://eslint.org/docs/latest/)
- ESLint + Playwright plugin [https://github.com/playwright-community/eslint-plugin-playwright](https://github.com/playwright-community/eslint-plugin-playwright)
- Gherkin notation [https://www.guru99.com/gherkin-test-cucumber.html](https://www.guru99.com/gherkin-test-cucumber.html)
- Playwright release notes [https://playwright.dev/docs/release-notes](https://playwright.dev/docs/release-notes)
