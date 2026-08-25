## What is SW Testing?
It is the systematic process of evaluating and verifying a software application to ensure it functions correctly, meets specified requirements, and is free of defects before relase


**Test Suite** : It is a arrangement of test cases that are developed to validate specific functionalities.Individual test cases in a suite are created to verify a particular functionality or performance goal

**Test Case** : It is a documented set of conditions, inputs, execution steps, and expected results used to verify that a specific feature or functionality of a software application behaves as intended.

**Test Script** : They describe a group of automated sequences of commands that are needed to execute a test case. They can be developed using multiple langues, and are utilized to automate the testing activities.

**Test Data** : They constitute the set of inputs required at the time of test execution. They play a very important role in verifying multiple scenarios and situations.

**Test Scenario**  : Its a high level description of a function or user flow that need to be validated, focusing on waht to test rather than how to test it.

**Positive Testing** : It is a software testing methodology that validates an application's functionality by providng **valid inputs** and verifying that the system behaves as expected under normal conditions. Also Known as **"Happy Path" testing**, It's primary goal is to confirm that the software meets its requirement and performs core functionality correctly when users follow intended workflows.

## Types of Test
- Unit Tests : Unit tests help catch bugs early in the development process.
- Integration Tests : It helps catch bugs when different units work together
- E2E Tests : It simulate use interactions with the entire system.

## What type of test to wright
- More Unit test than integration test.
- More Integration test than E2E test.

Based on their heigherarchy **test become slower** but **confidence level become higher**

## Testing Framework
A set of tools for writing and running tests

- Test Runner
- Assertion Libraries
- Mocking Tools
- Coverage Tools

Popular Frameworks : **Jest** (*Experimental* Support for ECMAScript Modules), **Mocha**, **Jasmine**, **Vitest**(Support ESM, Typescript and JSX), **Cypress**, **Playwright**

## How to structre a test

### AAA
- Arrange : Setup our test environment with necessary data or configs
- Act : Perform the action we test
- Assert : Check the outcome to match the expected

## TDD 
- Start by writing a failing test.
- Write just enough code to make the test pass.
- Refactor if necessary.
