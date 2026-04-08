# Test Plan — jAilbreak

## Table of contents

- [1. Introduction](#1-introduction)
  * [1.1 Purpose](#11-purpose)
  * [1.2 Scope](#12-scope)
  * [1.3 Intended Audience](#13-intended-audience)
  * [1.4 Document Terminology and Acronyms](#14-document-terminology-and-acronyms)
  * [1.5  References](#15--references)
  * [1.6 Document Structure](#16-document-structure)
- [2. Evaluation Mission and Test Motivation](#2-evaluation-mission-and-test-motivation)
  * [2.1 Background](#21-background)
  * [2.2 Evaluation Mission](#22-evaluation-mission)
  * [2.3 Test Motivators](#23-test-motivators)
- [3. Target Test Items](#3-target-test-items)
- [4. Outline of Planned Tests](#4-outline-of-planned-tests)
  * [4.1 Outline of Test Inclusions](#41-outline-of-test-inclusions)
  * [4.2 Outline of Other Candidates for Potential Inclusion](#42-outline-of-other-candidates-for-potential-inclusion)
  * [4.3 Outline of Test Exclusions](#43-outline-of-test-exclusions)
- [5. Test Approach](#5-test-approach)
  * [5.1 Initial Test-Idea Catalogs and Other Reference Sources](#51-initial-test-idea-catalogs-and-other-reference-sources)
  * [5.2 Testing Techniques and Types](#52-testing-techniques-and-types)
    + [5.2.1 Data and Database Integrity Testing](#521-data-and-database-integrity-testing)
    + [5.2.2 Functional Testing](#522-functional-testing)
    + [5.2.3 Business Cycle Testing](#523-business-cycle-testing)
    + [5.2.4 User Interface Testing](#524-user-interface-testing)
    + [5.2.5 Performance Profiling](#525-performance-profiling)
    + [5.2.6 Load Testing](#526-load-testing)
    + [5.2.7 Stress Testing](#527-stress-testing)
    + [5.2.8 Volume Testing](#528-volume-testing)
    + [5.2.9 Security and Access Control Testing](#529-security-and-access-control-testing)
    + [5.2.10 Failover and Recovery Testing](#5210-failover-and-recovery-testing)
    + [5.2.11 Configuration Testing](#5211-configuration-testing)
    + [5.2.12 Installation Testing](#5212-installation-testing)
- [6. Entry and Exit Criteria](#6-entry-and-exit-criteria)
  * [6.1 Test Plan](#61-test-plan)
    + [6.1.1 Test Plan Entry Criteria](#611-test-plan-entry-criteria)
    + [6.1.2 Test Plan Exit Criteria](#612-test-plan-exit-criteria)
    + [6.1.3 Suspension and Resumption Criteria](#613-suspension-and-resumption-criteria)
  * [6.2 Test Cycles](#62-test-cycles)
      - [6.2.1 Test Cycle Entry Criteria](#621-test-cycle-entry-criteria)
      - [6.2.2 Test Cycle Exit Criteria](#622-test-cycle-exit-criteria)
      - [6.2.3 Test Cycle Abnormal Termination](#623-test-cycle-abnormal-termination)
- [7. Deliverables](#7-deliverables)
- [7.1 Test Evaluation Summaries](#71-test-evaluation-summaries)
- [7.2 Reporting on Test Coverage](#72-reporting-on-test-coverage)
- [7.3 Perceived Quality Reports](#73-perceived-quality-reports)
- [7.4 Incident Logs and Change Requests](#74-incident-logs-and-change-requests)
- [7.5 Smoke Test Suite and Supporting Test Scripts](#75-smoke-test-suite-and-supporting-test-scripts)
- [7.6      Additional Work Products](#76------additional-work-products)
  * [7.6.1     Detailed Test Results](#761-----detailed-test-results)
  * [7.6.2     Additional Automated Functional Test Scripts](#762-----additional-automated-functional-test-scripts)
  * [7.6.3     Test Guidelines](#763-----test-guidelines)
  * [7.6.4     Traceability Matrices](#764-----traceability-matrices)
- [8. Testing Workflow](#8-testing-workflow)
- [9. Environmental Needs](#9-environmental-needs)
  * [9.1 Base System Hardware](#91-base-system-hardware)
  * [9.2 Base Software Elements in the Test Environment](#92-base-software-elements-in-the-test-environment)
  * [9.3 Productivity and Support Tools](#93-productivity-and-support-tools)
  * [9.4 Test Environment Configurations](#94-test-environment-configurations)
- [10. Responsibilities, Staffing, and Training Needs](#10-responsibilities--staffing--and-training-needs)
  * [10.1 People and Roles](#101-people-and-roles)
  * [10.2 Staffing and Training Needs](#102-staffing-and-training-needs)
- [11. Iteration Milestones](#11-iteration-milestones)
- [12. Risks, Dependencies, Assumptions, and Constraints](#12-risks--dependencies--assumptions--and-constraints)
- [13. Management Process and Procedures](#13-management-process-and-procedures)

## 1. Introduction

### 1.1 Purpose

The purpose of this Test Plan is to gather all the information needed to plan and control the test effort for jAilbreak. It describes the approach to testing the software.
This Test Plan supports the following objectives:

- Identifies the items that should be targeted by the tests.
- Identifies the motivation for and ideas behind the test areas to be covered.
- Outlines the testing approach that will be used.
- Identifies the required resources and provides an estimate of the test efforts.

### 1.2 Scope

This test plan covers the following levels and types of testing for jAilbreak:

- Unit testing of the Rust backend (route handlers, business logic, sort key generation)
- Database integrity testing (schema conformance, foreign key validation against live DynamoDB)
- Functional / BDD testing of the React frontend using Cucumber.js and Puppeteer
- API testing is a candidate for future inclusion as a third test type

Performance, load, stress, and volume testing are out of scope for this project given the team size and the serverless (AWS Lambda) nature of the deployment — AWS handles scaling for us.

### 1.3 Intended Audience

This document is intended for:

- Our project team members who need to understand the testing strategy
- Our professor and course evaluators reviewing the project's test coverage
- Future contributors who want to understand how tests are structured and run

### 1.4 Document Terminology and Acronyms

| Abbr  | Abbreviation                        |
|-------|-------------------------------------|
| API   | Application Programmable Interface  |
| BDD   | Behavior Driven Development         |
| CI    | Continuous Integration              |
| CD    | Continuous Delivery/Deployment      |
| CSS   | Cascading Style Sheets              |
| DB    | Database                            |
| FK    | Foreign Key                         |
| n/a   | not applicable                      |
| SRS   | Software Requirements Specification |
| tbd   | to be determined                    |
| UI    | User Interface                      |
| VC    | Version Control                     |
| VRM   | Virtual Reality Model               |
| VRMA  | VRM Animation                       |

### 1.5  References

| Title                                                                                                              | Date       | Publishing organization   |
|--------------------------------------------------------------------------------------------------------------------|:----------:| ------------------------- |
| [Blog Post — Unit Tests & VRM Model](../blog-unit-tests.md)                                                       | Apr. 2026  | jAilbreak Team            |
| [GitHub Repository](https://github.com/Tam-DHBW/jAilbreak)                                                        | Apr. 2026  | jAilbreak Team            |
| [Backend Unit Tests](https://github.com/Tam-DHBW/jAilbreak/tree/main/backend/jb_api/src)                          | Apr. 2026  | jAilbreak Team            |
| [Frontend Feature Files](https://github.com/Tam-DHBW/jAilbreak/tree/main/frontend/features)                       | Apr. 2026  | jAilbreak Team            |
| [Cargo.toml (build/dependency file)](https://github.com/Tam-DHBW/jAilbreak/blob/main/backend/jb_api/Cargo.toml)   | Apr. 2026  | jAilbreak Team            |
| [package.json (frontend dependencies)](https://github.com/Tam-DHBW/jAilbreak/blob/main/frontend/package.json)     | Apr. 2026  | jAilbreak Team            |

### 1.6 Document Structure

This document follows the standard RUP Test Plan template structure. Sections that are not applicable to our project are marked with "n/a" but the section numbering is kept intact as required.


## 2. Evaluation Mission and Test Motivation

### 2.1 Background

jAilbreak is a browser-based game where players interact with an AI "gatekeeper" character and try to extract passwords to progress through levels. The backend is written in Rust, deployed as AWS Lambda functions behind API Gateway, with DynamoDB as the database. The frontend is a React SPA with a Matrix/hacker theme, featuring a live 3D VRM avatar.

Testing is important for us because the backend handles real user data and game state in DynamoDB, and bugs in password validation or level progression would directly break the gameplay. Since we deploy to AWS Lambda, we can't just "quickly check" things on a dev server — we need confidence that the code works before it goes out. The frontend BDD tests help us verify that the core user flows (chatting with the gatekeeper, selecting levels, progressing through the game) actually work end-to-end.

### 2.2 Evaluation Mission

Our testing effort focuses on:

- Finding bugs in critical backend logic (password validation, level retrieval, sort key generation)
- Verifying that our DynamoDB schema stays in sync with our Rust structs
- Catching broken foreign key references in DynamoDB (since DynamoDB doesn't enforce FKs itself)
- Making sure the core frontend user flows work as expected
- Preventing regressions when we add new features

### 2.3 Test Motivators

- Quality risks: DynamoDB has no schema enforcement, so our data could drift out of sync with the code
- Functional requirements: password validation must be correct, level progression must work
- Technical risks: mocking AWS services correctly so tests are reliable
- Use cases: chat interaction, level selection, level progression

## 3. Target Test Items

The following items are targets for testing:

- **Backend API routes** (`jb_api`): `get_levels`, `validate_password`, and related handlers
- **Database layer** (`jb_api/src/db/`): schema conformance of `Level`, `Counter`, `PromptComponent` tables; foreign key integrity between levels and prompt components
- **Business logic**: sort key generation for prompt component ordering (`create_sort_key_between`)
- **Frontend user flows**: page loading, chat interaction, level selection, level progression

## 4. Outline of Planned Tests

### 4.1 Outline of Test Inclusions

*Frontend (React SPA)*:

- BDD / functional testing with Cucumber.js + Puppeteer
- Feature files covering: chat, level selection, level progression, basic page load

*Backend (Rust / AWS Lambda)*:

- Unit testing of route handlers with mocked DynamoDB (`aws-smithy-mocks`)
- Unit testing of pure business logic (sort key generation)
- Database integrity testing against live DynamoDB (schema conformance, FK checks)

The tests themselves will not be tested and will not count toward code coverage.

### 4.2 Outline of Other Candidates for Potential Inclusion

- API testing (sending HTTP requests to the deployed Lambda endpoints and validating responses) — this is a strong candidate for our third test type
- Integration testing of the full request flow through the Axum router

### 4.3 Outline of Test Exclusions

- Performance / load / stress / volume testing — our backend runs on AWS Lambda which auto-scales, so these tests don't add much value for our use case. There are also insufficient resources on our team to set up proper load testing infrastructure.
- Installation testing — the app is a web application, there's nothing to install on the user side.
- Configuration testing — we target modern browsers only, and the backend runs in a controlled AWS environment.
- Failover and recovery testing — AWS handles this at the infrastructure level for Lambda and DynamoDB.

## 5. Test Approach

### 5.1 Initial Test-Idea Catalogs and Other Reference Sources

- The game's use cases (chat with gatekeeper, validate password, progress through levels) directly informed which tests to write
- DynamoDB's lack of schema/FK enforcement motivated the database integrity tests
- The Cucumber.js feature files serve as living documentation of expected frontend behavior

### 5.2 Testing Techniques and Types

#### 5.2.1 Data and Database Integrity Testing

|                       | Description                                                         |
|-----------------------|---------------------------------------------------------------------|
|Technique Objective    | Verify that DynamoDB table contents match our Rust struct definitions, and that all foreign key references between tables are valid. |
|Technique              | Use `serde-reflection` to extract expected field names from Rust structs at test time. Scan each DynamoDB table and compare actual item keys against expected fields. For FK checks, scan levels and verify that every referenced `prompt_component` ID and `next` level ID exists in the respective tables. |
|Oracles                | Tests are self-verifying: `assert!` macros compare expected vs actual field sets and report any missing/extra fields or dangling FK references. |
|Required Tools         | Rust built-in test framework, `serde-reflection` crate, `aws-sdk-dynamodb`, live DynamoDB access (behind `local-testing` feature flag) |
|Success Criteria       | All schema conformance tests pass (no missing or extra fields). All FK integrity tests pass (no dangling references). |
|Special Considerations | These tests require AWS credentials and access to the actual DynamoDB tables. They run behind a Cargo feature flag (`local-testing`) so they don't execute in normal `cargo test` runs. |

#### 5.2.2 Functional Testing

|                       | Description                                                         |
|-----------------------|---------------------------------------------------------------------|
|Technique Objective    | Verify that core game functionality works correctly: chat interaction, level selection, level progression, password validation. |
|Technique              | BDD approach using Cucumber.js with Gherkin feature files. Puppeteer drives a headless browser to interact with the React frontend. Backend route handlers are tested directly by calling the Axum handler functions with mocked DynamoDB clients. |
|Oracles                | Frontend: Cucumber step definitions assert on DOM state (elements exist, content matches). Backend: Rust `assert_eq!` / `assert!` macros verify return values from handler functions. |
|Required Tools         | Frontend: Cucumber.js (`@cucumber/cucumber`), Puppeteer. Backend: Rust test framework, `aws-smithy-mocks` for DynamoDB mocking. |
|Success Criteria       | All feature scenarios pass. All backend unit tests for route handlers pass. |
|Special Considerations | Frontend BDD tests need the app to be running (or a built version served). Backend mocked tests run fully offline with no AWS access needed. |

#### 5.2.3 Business Cycle Testing

n/a — not applicable for a game application with no recurring business cycles.

#### 5.2.4 User Interface Testing

|                       | Description                                                         |
|-----------------------|---------------------------------------------------------------------|
|Technique Objective    | Verify that the game UI renders correctly and users can navigate through the core flows. |
|Technique              | Covered by our Cucumber.js BDD tests which use Puppeteer to interact with the actual UI in a headless browser. Feature files define scenarios like "I click on a level → chat history should be cleared". |
|Oracles                | Puppeteer assertions check for presence of DOM elements, text content, and UI state changes. |
|Required Tools         | Cucumber.js, Puppeteer, Vite dev server |
|Success Criteria       | All UI-related feature scenarios pass. |
|Special Considerations | The 3D VRM model rendering is not tested automatically — it requires visual inspection. |

#### 5.2.5 Performance Profiling

n/a — AWS Lambda handles scaling. Not in scope for this project.

#### 5.2.6 Load Testing

n/a — AWS Lambda auto-scales. Not in scope for this project.

#### 5.2.7 Stress Testing

n/a — insufficient resources to conduct these tests, and AWS Lambda handles resource management.

#### 5.2.8 Volume Testing

n/a — our DynamoDB tables are small (handful of levels and prompt components). Volume testing is not relevant.

#### 5.2.9 Security and Access Control Testing

|                       | Description                                                         |
|-----------------------|---------------------------------------------------------------------|
|Technique Objective    | Ensure that only authenticated users can access protected API endpoints, and that the admin panel is restricted to authorized users. |
|Technique              | We have a custom Lambda authorizer (`jb_authorizer`) that validates Cognito JWT tokens. Access control is enforced at the API Gateway level. Manual testing is done by attempting API calls with and without valid tokens. |
|Oracles                | Unauthorized requests return 401/403 responses. Authorized requests succeed. |
|Required Tools         | Manual testing with curl/Postman, AWS Cognito |
|Success Criteria       | Unauthenticated requests are rejected. Authenticated requests with valid tokens succeed. |
|Special Considerations | Automated security testing is not yet implemented. The authorizer logic could be unit tested in the future. |

#### 5.2.10 Failover and Recovery Testing

n/a — AWS manages failover for Lambda and DynamoDB. Not in scope.

#### 5.2.11 Configuration Testing

n/a — web application targeting modern browsers. Backend runs in a controlled AWS environment.

#### 5.2.12 Installation Testing

n/a — web application, nothing to install on the client side. Backend deployment is handled via `cargo lambda deploy`.


## 6. Entry and Exit Criteria

### 6.1 Test Plan

#### 6.1.1 Test Plan Entry Criteria

- The feature or fix is implemented and compiles without errors
- For backend tests: the code is merged into the working branch
- For frontend BDD tests: the app can be built and served locally

#### 6.1.2 Test Plan Exit Criteria

- All unit tests pass (`cargo test` / `just b_test`)
- All BDD feature scenarios pass (`cucumber-js` / `just f_bdd`)
- No critical or high-severity defects remain open

#### 6.1.3 Suspension and Resumption Criteria

- Testing is suspended if AWS credentials expire or DynamoDB is unreachable (for database tests)
- Testing resumes once access is restored
- Mocked unit tests are not affected by AWS availability

### 6.2 Test Cycles

##### 6.2.1 Test Cycle Entry Criteria

- Code compiles successfully
- All dependencies are installed (`cargo build` / `npm install`)

##### 6.2.2 Test Cycle Exit Criteria

- All tests in the cycle have been executed
- Results have been reviewed

##### 6.2.3 Test Cycle Abnormal Termination

- If AWS services are down, database integrity tests are skipped
- Mocked unit tests and frontend BDD tests can still run independently


## 7. Deliverables

## 7.1 Test Evaluation Summaries

Test results are printed to the terminal when running `just b_test` (backend) or `just f_bdd` (frontend). Cucumber.js also generates an HTML report at `frontend/reports/cucumber-report.html`.

## 7.2 Reporting on Test Coverage

Backend code coverage can be measured using `cargo-tarpaulin` or `cargo-llvm-cov`. We aim to cover the critical paths: password validation, level retrieval, sort key logic, and database schema conformance. Coverage reports are generated on demand.

## 7.3 Perceived Quality Reports

n/a

## 7.4 Incident Logs and Change Requests

Bugs and issues are tracked via GitHub Issues on the [jAilbreak repository](https://github.com/Tam-DHBW/jAilbreak/issues). Pull requests reference related issues when fixing bugs found through testing.

## 7.5 Smoke Test Suite and Supporting Test Scripts

The `simple-test.feature` file serves as a basic smoke test — it just verifies that the page loads successfully. For the backend, running `cargo test` without the `local-testing` feature flag executes only the mocked unit tests, which serves as a quick smoke test.

## 7.6      Additional Work Products

### 7.6.1     Detailed Test Results

Test output is captured in the terminal. Cucumber HTML reports are generated at `frontend/reports/cucumber-report.html`.

### 7.6.2     Additional Automated Functional Test Scripts

- Backend test files: [`backend/jb_api/src/db/tests.rs`](https://github.com/Tam-DHBW/jAilbreak/blob/main/backend/jb_api/src/db/tests.rs), [`backend/jb_api/src/db/prompt.rs`](https://github.com/Tam-DHBW/jAilbreak/blob/main/backend/jb_api/src/db/prompt.rs) (test module), [`backend/jb_api/src/routes/levels/mod.rs`](https://github.com/Tam-DHBW/jAilbreak/blob/main/backend/jb_api/src/routes/levels/mod.rs) (test module), [`backend/jb_api/src/routes/levels/validate.rs`](https://github.com/Tam-DHBW/jAilbreak/blob/main/backend/jb_api/src/routes/levels/validate.rs) (test module)
- Frontend feature files: [`frontend/features/`](https://github.com/Tam-DHBW/jAilbreak/tree/main/frontend/features)

### 7.6.3     Test Guidelines

- Backend unit tests live next to the code they test, inside `#[cfg(test)] mod tests { }` blocks — this is the standard Rust convention
- Database tests are gated behind the `local-testing` feature flag so they don't run without AWS access
- Frontend BDD tests follow the Gherkin syntax and step definitions live in `frontend/features/support/`

### 7.6.4     Traceability Matrices

n/a


## 8. Testing Workflow

1. Developer writes or modifies code
2. Developer runs `just b_test` to execute backend tests (mocked unit tests always, database tests if AWS credentials are available)
3. Developer runs `just f_bdd` to execute frontend BDD tests
4. If all tests pass, the code is committed and pushed
5. Code review on the pull request
6. Merge to main

For the backend, Rust's built-in test framework discovers all `#[test]` and `#[tokio::test]` functions automatically. For the frontend, Cucumber.js picks up all `.feature` files from `frontend/features/` and matches them to step definitions in `frontend/features/support/`.

## 9. Environmental Needs

### 9.1 Base System Hardware

| Resource                                | Quantity | Name and Type                          |
|-----------------------------------------|----------|----------------------------------------|
| Database                                | 3 tables | AWS DynamoDB (Levels, PromptComponents, Counters) |
| Backend compute                         | 3        | AWS Lambda functions (api_regular, api_chat, authorizer) |
| Frontend hosting                        | 1        | AWS S3 bucket + CloudFront             |
| Developer machines                      | 2        | macOS (Apple Silicon)                  |

### 9.2 Base Software Elements in the Test Environment

| Software Element Name    | Type and Other Notes                                      |
|--------------------------|-----------------------------------------------------------|
| Rust toolchain           | Compiler + built-in test framework (`cargo test`)         |
| cargo-lambda             | Build tool for AWS Lambda Rust functions                  |
| aws-smithy-mocks 0.2    | AWS SDK mocking library for unit tests                    |
| serde-reflection 0.5     | Struct introspection for schema conformance tests         |
| Node.js                  | Runtime for frontend tooling                              |
| Cucumber.js 12.2         | BDD test framework with Gherkin syntax                    |
| Puppeteer 24.x           | Headless browser automation for frontend tests            |
| Vite 4.x                 | Frontend dev server / build tool                          |

### 9.3 Productivity and Support Tools

| Tool Category or Type             | Tool Brand Name                  | Vendor or In-house | Version   |
|-----------------------------------|----------------------------------|--------------------|-----------|
| Version Control                   | Git + GitHub                     | GitHub             | -         |
| Build system (backend)            | Cargo + cargo-lambda             | Rust / AWS         | latest    |
| Build system (frontend)           | Vite                             | Open source        | 4.x       |
| Task runner                       | just (justfile)                  | Open source        | latest    |
| IDE                               | VS Code / Kiro                   | Microsoft / AWS    | latest    |
| Infrastructure as Code            | Terraform                        | HashiCorp          | latest    |
| BDD test reports                  | Cucumber HTML Reporter           | Open source        | -         |

### 9.4 Test Environment Configurations

| Configuration Name                | Description                                              | Implemented in Physical Configuration |
|-----------------------------------|----------------------------------------------------------|---------------------------------------|
| Local development                 | macOS with Rust toolchain, Node.js, AWS CLI configured   | Developer MacBooks                    |
| Mocked backend tests              | No AWS access needed, runs fully offline                 | Any machine with Rust installed       |
| Database integration tests        | Requires AWS credentials and DynamoDB access             | Developer machines with `mwinit` auth |

## 10. Responsibilities, Staffing, and Training Needs

### 10.1 People and Roles

| Role              | Person / Allocation | Specific Responsibilities                                                    |
|-------------------|---------------------|------------------------------------------------------------------------------|
| Backend Developer & Tester | Tam       | Writes backend code and unit tests, database integrity tests, maintains Cargo.toml dependencies |
| Frontend Developer & Tester | Team     | Writes frontend code and Cucumber BDD feature files, maintains step definitions |
| Test Reviewer     | All team members    | Reviews test code in pull requests, verifies test results                     |

### 10.2 Staffing and Training Needs

We're a small university project team, so everyone wears multiple hats. No dedicated test staff. Training needs are minimal — Rust's test framework is straightforward, and Cucumber.js has good documentation. The main learning curve was figuring out `aws-smithy-mocks` for mocking DynamoDB in the backend tests.

## 11. Iteration Milestones

We want to keep covering the critical backend paths: password validation, level retrieval, database schema conformance, and FK integrity. As we add new routes or business logic, corresponding unit tests should be added. Frontend BDD coverage should grow as new user-facing features are implemented.

## 12. Risks, Dependencies, Assumptions, and Constraints

| Risk                                                        | Mitigation Strategy                                                              | Contingency (Risk is realized)                                                |
|-------------------------------------------------------------|----------------------------------------------------------------------------------|-------------------------------------------------------------------------------|
| AWS credentials expire, database tests can't run            | Use `mwinit` to refresh credentials before test runs                             | Skip database tests, rely on mocked unit tests                                |
| DynamoDB schema changes without updating Rust structs       | Schema conformance tests catch this automatically                                | Fix the struct or the table, re-run tests                                     |
| Frontend BDD tests break due to UI changes                  | Keep step definitions loosely coupled to specific CSS selectors                  | Update step definitions to match new UI                                       |
| Mocked tests don't catch real AWS SDK behavior differences  | Supplement with database integration tests that hit real DynamoDB                 | Investigate failures in production, add regression tests                      |
| Puppeteer/browser version incompatibility                   | Pin Puppeteer version in package.json                                            | Update Puppeteer and fix any breaking changes in step definitions             |

## 13. Management Process and Procedures

n/a — we're a small team. Test execution is part of the regular development workflow. Every developer runs tests locally before pushing (in theory). Code reviews (if we will ever do them) check that tests are included for new functionality.
