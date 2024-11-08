# Code Owners

The CODEOWNERS.md file is a convention in Xempus to try to clarify who is responsible for reviewing and approving changes to specific parts of the codebase. This file helps streamline the code review process and ensures that changes are reviewed by the appropriate stakeholders before being merged into the main branch.

## Example of a CODEOWNERS.md file from Playwright project

```markdown
Every individual with the according Bitbucket permissions is allowed to contribute to this project.

Please keep in mind, that in contrast to other repositories every engineer can push changes to the main branch without a pull request;
(aka trunk-based development) therefore special care is required here.

This file provides an up-to-date list of the Code Owners, who are consultants or/and main Code Reviewers in case of a complex change.

Please check out CONTRIBUTION_POLICY.md for information on how to contribute. In case of doubt, please get in touch with the QA-Chapters Lead.

Note: email-addresses are not fully specified, you have to add the @xempus.com after the username

## GLOBAL

Everything that is not specified defaults to the QA-Chapter Lead: thomas.laffleur

## components

./components/advisor **bruno.palma junaed.tariq anna.dovzhyk olena.khomenko bojan.harjac jasmine.baral**
./components/budget-berater **alexander.kolp**
./components/consumer **elias.rudakov hosnia.najem**
./components/manager **elias.rudakov hosnia.najem**
./components/universal **bruno.palma manonmani.ramu**

## config

./config **bruno.palma hosnia.najem**

## data

./data/enums **elias.rudakov hosnia.najem**

## docs

./docs **bruno.palma manonmani.ramu hosnia.najem jasmine.baral**

## Jenkins / CI
```

./jenkins **hosnia.najem manonmani.ramu**

## scripts

./scripts **manonmani.ramu bruno.palma**

## test-suites

./test-suites **bruno.palma hosnia.najem**
./test-suites/contract.ts **manonmani.ramu bruno.palma**

## tests

./tests/advisor **bruno.palma junaed.tariq anna.dovzhyk olena.khomenko bojan.harjac jasmine.baral**
./tests/agent **bruno.palma junaed.tariq anna.dovzhyk olena.khomenko bojan.harjac jasmine.baral**
./tests/agent-aks **junaed.tariq**
./tests/agent-manager **elias.rudakov hosnia.najem**
./tests/budget-berater **alexander.kolp**
./tests/consumer **elias.rudakov hosnia.najem**
./tests/consumer/postbox **manonmani.ramu**
./tests/employee **elias.rudakov hosnia.najem**
./tests/employer **elias.rudakov hosnia.najem**
./test/load **bruno.palma**
./tests/manager **elias.rudakov hosnia.najem**
./tests/manager/postbox **manonmani.ramu**
./tests/platform \*\*hosnia.najem\*\*

## types

./types **bruno.palma hosnia.najem**

For more options please check out a Github example

<https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-code-owners>
