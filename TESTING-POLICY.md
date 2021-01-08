# Testing Policy

## Scope and Overview

The testing policy describes the high level approach that will be undertaken towards System and Software Testing. It describes the test approach, the test environment, testing tools, release control, risk analysis and review and approvals.

## Test Approach

* To plan testing early in the project so that testing activities may be started as soon as possible in the project life cycle, and resources planned accordingly.
* To follow a test-driven approach that focuses on the desired functionality of the application as well as other aspects such as program structure and readability. 
* To adopt a risk-based approach to testing to help target, focus and prioritize testing with the added benefit of making efficient use of resources.
* To focus on ensuring defect discovery (be they code defects, requirement defects etc.) takes place as soon as possible to prevent the escalating costs of identifying and fixing bugs later on in the project/software lifecycle. 
* Ensuring full traceability of testing coverage back to original functional requirements to ensure key functional requirements are covered by testing.


## Test Environment

* OpenJDK 14
* Docker in Docker
* Gitlab CI/CD


## Testing Tools

* Unit and integration testing:
    * [Gradle](https://gradle.org/)
      * Used to build the application and create tasks for tests that execute in a specific order.
    * [Ktlint](https://ktlint.github.io/)
      * "An anti-bikeshedding Kotlin linter with built-in formatter" used to format the Kotlin code in our project in order to maintain consistency accross all authors.
    * [Mockk](https://mockk.io/)
      * Used during API unit tests to mock services and repositories.
    * [Kotest](https://kotest.io/)
      * The test runner used by the API to execute unit and integration tests.
    * [Mockito](https://site.mockito.org/)
      * "Tasty mocking framework for unit tests in Java". This framework is used to test our Java code in our **optimizer** repository.
    * [JUnit](https://junit.org)
      * Testing platform used in conjunction with Mockito in order to create unit tests in Java.
* Non functional requirements testing:
    * [Sonar Cloud](https://sonarcloud.io/) (maintainability testing/analysis)
      * Sonar cloud is used to analyze and grade the API codebase to identify code smells and technical debt which provides you with an idea of how **maintainable** your project is.
      * Used to analyze and grade the API codebase to identify **security** vulnerabilities and poor code practices.
    * [Litmus](https://litmuschaos.io/)
      * Used with Kubernetes for chaos testing, by executing and analysising chaos tests you are able to verify the reliability of a system.
    * [JaCoCo](https://www.eclemma.org/jacoco/)
      * Used to generate code coverage reports for the API codebase.

## Release Control

#### Versioning

Our **api** and **optimizer** repositories make use of a plugin called _semantic-release_ in order to automatically generate a CHANGELOG, tag and release on each relevant merge commit. The entries in the CHANGELOG and the descriptions of our release are determined by the commit messages introduced in each merge request. The following version bumps occur based on the conventional commits in the git history since the latest release.

Furthermore, these projects use the SemVer schema and the following commits cause major release version bumps based on the following commit types:

* _fix_ - bumps patch version
* _feat_ - bumps minor version
* _BREAKING CHANGE_ - bumps major version

Furthermore, these repositories follow the SemVer schema, vX.X.X. 

New releases on the **alpha** branch take the following form:

`1.0.0-alpha.1`

and on **beta**:

`1.0.0-beta.1`

#### Commit Control

**Conventional Commits** is used as a commit naming guideline for this repository. For more information on this, please
visit the following [link](https://www.conventionalcommits.org/en/v1.0.0-beta.3/).  
_Note that GitLab automatically links commits to issues when an issue number is referenced with `#<issue no.>`_

Each commit message follows the pattern:

Regex: `(build|chore|ci|docs|feat|fix|perf|refactor|style|test)(\(#\d+\))?: (.+)((\n\n|.)+)`

Simplified Pattern: `<type>(<optional scope>): <description>`

In order to indicate a breaking change or a closed issue, the following applies:

```
<type>(<optional scope>): <description>

BREAKING CHANGE: <description>

Closes #<issue no.>
```

## Risk Analysis

Sonar Cloud (used for code analysis and code coverage reporting) runs on both the **api** and **optimizer** repositories whenever a new merge is created, this provides a report which is linked to the merge via an automated commit. Part of this report includes a security analysis


## Review and Approvals

When making a merge request, the pipeline must **pass** in order for the merge request to be permitted. The following rules apply:

* All protected pre-release branches (**alpha** and **beta**) require at least one approval, not including the author, in order to accept a merge request. This ensures that before any code is moved into the development branch it is reviewed by at least one other member of the team. 
* Merges made into the **master** branch of requires approval of all three of the project owners (the Truckin-IT project clients).