# ParaBank QA Automation: Customer Login Feature

This repository contains the Quality Assurance documentation for the **Customer Login** feature of the ParaBank application. It includes the Software Test Plan (STP) and the Functional Requirements Document (FRD) that guide the testing efforts.

## Project Details

| **Attribute**        | **Details**              |
| -------------------- | ------------------------ |
| **Project**          | ParaBank QA Automation   |
| **Feature**          | Customer Login           |
| **Author**           | Baseeil Jaber           |
| **Date**             | August 10, 2025          |
| **Version**          | 1.1                      |

## Table of Contents
*   [Software Test Plan (STP)](#software-test-plan-stp)
    *   [1. Introduction](#1-introduction)
    *   [2. Test Team](#2-test-team)
    *   [3. Test Objectives](#3-test-objectives)
    *   [4. Scope](#4-scope)
    *   [5. Test Approach](#5-test-approach)
    *   [6. Test Environment](#6-test-environment)
    *   [7. Test Cases Reference](#7-test-cases-reference)
    *   [8. Test Deliverables](#8-test-deliverables)
    *   [9. Schedule](#9-schedule)
    *   [10. Risks & Mitigation](#10-risks--mitigation)
*   [Functional Requirements Document (FRD)](#functional-requirements-document-frd)
    *   [1. Feature Overview](#1-feature-overview)
    *   [2. Objectives](#2-objectives)
    *   [3. Functional Requirements](#3-functional-requirements)
    *   [4. Test Cases](#4-test-cases)
    *   [5. Security Considerations](#5-security-considerations)
    *   [6. Dependencies](#6-dependencies)
*   [ParaBank Login Test Suite - Postman Collection](#parabank-login-test-suite---postman-collection)
    *   [Features](#features)
    *   [Prerequisites](#prerequisites)
    *   [Setup and Configuration](#setup-and-configuration)
    *   [How to Use](#how-to-use)
    *   [Test Suite Structure](#test-suite-structure)
    *   [Collection Variables](#collection-variables)
*   [ParaBank Login API Test Suite (JMeter)](#parabank-login-api-test-suite-jmeter)
    *   [Overview](#overview)
    *   [Test Scenarios Included](#test-scenarios-included)
    *   [Excluded Scenarios (Manual/UI Tests)](#excluded-scenarios-manualui-tests)
    *   [How to Use](#how-to-use-1)
    *   [JMeter Plan Structure](#jmeter-plan-structure)
---

## Software Test Plan (STP)

This document defines the strategy, scope, and process for testing the Customer Login feature of the ParaBank application.

### 1. Introduction
This Software Test Plan (STP) defines the strategy, scope, and process for testing the Customer Login feature of the ParaBank application. Testing activities will be managed in `TestRail`, defect tracking will be handled via `Jira`, and API-level validations will be conducted using `Postman`. No other testing tools will be introduced.

### 2. Test Team
The testing team for this project is as follows:
- **Baseil Jaber** – Team Leader
- **Ali Abo Jafar** – QA Engineer
- **Abdelnaser** – QA Engineer
- **Ali Taha** – Project Monitor

### 3. Test Objectives
- Verify that valid login credentials successfully grant access to the account overview.
- Validate that incorrect login attempts produce correct error handling.
- Ensure compliance with accessibility and usability standards.
- Check security measures against SQL Injection, XSS, and brute-force attacks.
- Confirm proper logging and audit trails for all login attempts.

### 4. Scope
The scope of this test plan includes functional, non-functional, and security testing of the Customer Login feature. Testing will include UI validation, API validation, and integration with backend services. All tests will be designed and managed in `TestRail`, executed partially via `Postman` for API checks, and any issues will be logged in `Jira`.

### 5. Test Approach
Testing will follow a combination of manual UI testing and API-level testing using `Postman`. All test cases will be documented and managed in `TestRail`. Any identified defects will be logged and tracked in `Jira` until closure. Security testing will be performed manually with crafted payloads.

### 6. Test Environment
Testing will be conducted in the following environment:
- **Web browser compatibility:** Chrome, Firefox, Edge, Safari
- **Operating systems:** Windows 10/11, macOS, Android, iOS
- **Test server:** A dedicated server with a copy of the production database
- **Network:** Stable internet connection for HTTPS traffic
- **API Tool:** `Postman` configured with ParaBank API endpoints

### 7. Test Cases Reference

| TC ID | Description                                                    | Expected Result                                       |
| ----- | -------------------------------------------------------------- | ----------------------------------------------------- |
| TC01  | Login with valid username and password                         | User is redirected to account overview                |
| TC02  | Login with valid username and invalid password                 | Error message: “Invalid username or password”         |
| TC03  | Login with invalid username and valid password                 | Error message: “Invalid username or password”         |
| TC04  | Submit login form with empty fields                            | Validation message prompts user to enter credentials  |
| TC05  | Submit login form with whitespace-only input                   | Validation message prompts user to enter valid data   |
| TC06  | Click “Forgot login info?” link                                | Redirects to account recovery page                    |
| TC07  | Click “Register” link                                          | Redirects to new user registration page               |
| TC08  | Attempt login with SQL injection payload in username or password | Input rejected, error message shown                   |
| TC09  | Attempt login with XSS script in username or password          | Input sanitized, no script execution                  |
| TC10  | Enter password and verify masking                              | All characters hidden as ● or *                       |
| TC11  | Navigate form using only keyboard                              | All fields and buttons accessible in logical order    |
| TC12  | Access login page from mobile device                           | Page adapts to screen size with proper layout         |
| TC13  | Attempt login after 5 failed attempts                          | Account locked message displayed                      |
| TC14  | Verify audit log entry after login attempt                     | Entry recorded with timestamp, username, and status   |
| TC15  | Verify session management after successful login               | Session token generated and invalidated on logout     |

### 8. Test Deliverables
- Test Plan document (this STP)
- Test Cases in `TestRail`
- API test collections in `Postman`
- Defect Reports in `Jira`
- Test Execution Reports from `TestRail`
- Final Test Summary Report

### 9. Schedule
The test execution will be planned over a 2-week sprint:
- **Week 1:** Manual UI and API test execution & defect logging in `Jira`.
- **Week 2:** Regression testing in `TestRail` and API re-testing in `Postman`.

### 10. Risks & Mitigation

| Risk                           | Mitigation                                      |
| ------------------------------ | ----------------------------------------------- |
| Unavailability of test environment | Set up a backup test environment.               |
| Delayed delivery of build      | Adjust test schedule and prioritize critical cases. |
| Test data inconsistencies      | Maintain controlled and isolated test data sets.    |


---

## Functional Requirements Document (FRD)

This document outlines the functional requirements for the Customer Login feature.

### 1. Feature Overview
The Customer Login feature enables registered ParaBank customers to securely access their banking accounts using their username and password. It serves as the primary entry point for account-related operations, making its reliability, usability, and security essential to customer trust and regulatory compliance.

### 2. Objectives
- Validate the secure and accurate login process.
- Ensure proper handling of invalid or missing credentials.
- Confirm compliance with accessibility and usability standards.
- Test for resilience against common security threats (e.g., SQL Injection, XSS).
- Verify proper logging and audit trail creation for login attempts.

### 3. Functional Requirements

| ID   | Requirement Description                                                                |
| ---- | -------------------------------------------------------------------------------------- |
| FR1  | The login form must display **Username** and **Password** fields.                      |
| FR2  | A “**Login**” button must be provided to submit credentials.                             |
| FR3  | Credentials must be validated against the backend user database.                       |
| FR4  | Valid credentials must redirect the user to the account overview page.                 |
| FR5  | Invalid credentials must trigger a descriptive error message.                          |
| FR6  | A “**Forgot login info?**” link must navigate to the account recovery page.              |
| FR7  | A “**Register**” link must navigate to the new user registration page.                   |
| FR8  | The login form must be fully operable via keyboard navigation.                         |
| FR9  | The password field must mask all entered characters.                                   |
| FR10 | All login attempts must be recorded in the audit log.                                  |
| FR11 | Accounts must be temporarily locked after 5 consecutive failed login attempts.         |
| FR12 | The login page must be responsive on desktops, tablets, and mobile devices.            |
| FR13 | The login form must perform client- and server-side input validation.                  |
| FR14 | The system must sanitize inputs to prevent SQL Injection and XSS attacks.              |
| FR15 | Session tokens must be securely generated and invalidated upon logout.                 |

### 4. Test Cases
The following test cases are designed to validate the functional requirements.

| TC ID | Test Case Description                                          | Expected Result                                       |
| ----- | -------------------------------------------------------------- | ----------------------------------------------------- |
| TC01  | Login with valid username and password                         | User is redirected to account overview                |
| TC02  | Login with valid username and invalid password                 | Error message: “Invalid username or password”         |
| TC03  | Login with invalid username and valid password                 | Error message: “Invalid username or password”         |
| TC04  | Submit login form with empty fields                            | Validation message prompts user to enter credentials  |
| TC05  | Submit login form with whitespace-only input                   | Validation message prompts user to enter valid data   |
| TC06  | Click “Forgot login info?” link                                | Redirects to account recovery page                    |
| TC07  | Click “Register” link                                          | Redirects to new user registration page               |
| TC08  | Attempt login with SQL injection payload in username or password | Input rejected, error message shown                   |
| TC09  | Attempt login with XSS script in username or password          | Input sanitized, no script execution                  |
| TC10  | Enter password and verify masking                              | All characters hidden as ● or *                       |
| TC11  | Navigate form using only keyboard                              | All fields and buttons accessible in logical order    |
| TC12  | Access login page from mobile device                           | Page adapts to screen size with proper layout         |
| TC13  | Attempt login after 5 failed attempts                          | Account locked message displayed                      |
| TC14  | Verify audit log entry after login attempt                     | Entry recorded with timestamp, username, and status   |
| TC15  | Verify session management after successful login               | Session token generated and invalidated on logout     |

### 5. Security Considerations
- Enforce **HTTPS** for all login traffic.
- Sanitize and validate all user inputs on both the client and server.
- Protect against **SQL Injection**, **XSS**, and **brute force** attacks.
- Securely manage authentication tokens and session cookies.

### 6. Dependencies
- Active user account records in the database.
- Functional authentication service.
- ParaBank web application UI framework.
- Audit logging infrastructure.
---

# ParaBank Login Test Suite - Postman Collection

This repository contains a comprehensive Postman collection for testing the login functionality of the ParaBank application. It is designed to be a practical companion to the **Software Test Plan (STP)** and **Functional Requirements Document (FRD)**.

The collection covers functional, security, and integration scenarios via the ParaBank REST API. It includes a mix of fully automated API tests, API calls that support manual UI verification, and placeholders for tests that must be performed manually.

## Features

-   **Structured Test Suites:** Requests are organized into folders based on test type (Functional, Security, Usability, Backend).
-   **Direct Mapping to Test Cases:** Each request name is mapped to a Test Case ID (e.g., `C1 / TC01`) from the project's formal test documentation.
-   **Automated Validation:** JavaScript tests are embedded in requests to automatically assert response status, body content, and functional correctness.
-   **Security Penetration Tests:** Includes basic checks for common vulnerabilities like SQL Injection and XSS.
-   **Stateful Scenarios:** Demonstrates how to test features like session management and brute-force protection using Postman's scripting and Collection Runner.
-   **Clear Documentation:** Each request includes a detailed description of its objective, steps, and expected results.

## Prerequisites

1.  **Postman App:** You must have the [Postman Desktop App](https://www.postman.com/downloads/) installed.
2.  **Import the Collection:**
    -   Download the `ParaBank Login Test Suite.postman_collection.json` file.
    -   In Postman, click **Import** and upload the file.

## Setup and Configuration

The collection uses a single collection-level variable to manage the target environment.

-   `{{baseUrl}}`: The base URL for the ParaBank API.
    -   **Default Value:** `https://parabank.parasoft.com/parabank/services/bank`
    -   You can edit this variable in the collection's "Variables" tab to point to a local or different staging environment.

## How to Use

### 1. Running Individual Requests

You can run any request individually by selecting it and clicking **Send**. After the request completes, check the **Tests** tab in the response pane to see the results of the automated assertions.

### 2. Running the Full Suite (or Folders)

For stateful tests that must run in sequence (like **Account Lockout** or **Session Management**), you must use the Collection Runner.

1.  Hover over the collection or a specific folder and click the **▶ Run** button.
2.  The Collection Runner window will open.
3.  Ensure the requests are in the correct order.
4.  Click **Run ParaBank Login Test Suite**.
5.  The runner will execute all requests and display a summary of the test results.

---

## Test Suite Structure

The collection is organized into the following test suites:

### 📁 Functional Tests

Tests covering the core functionality of the login process.

| Test Case ID | Request Name / Objective                                | Type                | Key Checks / Notes                                                 |
| :----------- | :------------------------------------------------------ | :------------------ | :----------------------------------------------------------------- |
| `C1 / TC01`  | Login with valid username and password                  | API (Automated)     | Verifies 200 OK status and that the response contains customer XML. Saves `customerId` for other tests. |
| `C2 / TC02`  | Login with valid username and invalid password          | API (Automated)     | Verifies the response contains the "Invalid username and password" error message. |
| `C3 / TC03`  | Login with invalid username and valid password          | API (Automated)     | Verifies the response contains the "Invalid username and password" error message. |
| `C4 / TC04`  | Submit login form with empty fields                     | API (Automated)     | Verifies that an invalid URL path results in a 404 Not Found error. |
| `C5 / TC05`  | Submit login form with whitespace-only input            | API (Automated)     | Verifies the system treats whitespace as invalid credentials and shows an error. |
| `C6 / TC06`  | Click “Forgot login info?” link (API Alternative)       | API (Manual Check)  | Tests the underlying customer lookup API that the UI feature depends on. |
| `C7 / TC07`  | Click “Register” link                                   | **Manual / UI Test**| Placeholder to remind the tester to verify the 'Register' link navigation in the browser. |

### 📁 Security Tests

Tests for common security vulnerabilities.

| Test Case ID | Request Name / Objective                                | Type                 | Key Checks / Notes                                                 |
| :----------- | :------------------------------------------------------ | :------------------- | :----------------------------------------------------------------- |
| `C8 / TC08`  | Attempt login with SQL injection payload                | API (Automated)      | Verifies the application rejects the input gracefully and does **not** return a 500 error. |
| `C9 / TC09`  | Attempt login with XSS script payload                   | API (Automated)      | Verifies the application sanitizes the input, fails the login, and does **not** return a 500 error. |
| `C10 / TC13` | Account lockout after 5 failed login attempts           | API (Stateful)       | **Requires Collection Runner.** Simulates 5 failed attempts and checks the 6th. |

### 📁 Usability & Accessibility Tests

Placeholders for manual UI-based tests.

| Test Case ID | Request Name / Objective                     | Type                 | Key Checks / Notes                                                 |
| :----------- | :------------------------------------------- | :------------------- | :----------------------------------------------------------------- |
| `C11 / TC10` | Verify password masking                      | **Manual / UI Test** | Manually verify that characters typed in the password field are obscured. |
| `C12 / TC11` | Navigate form using only keyboard            | **Manual / UI Test** | Manually verify all form elements are focusable in a logical order using the Tab key. |
| `C13 / TC12` | Responsive design on mobile device           | **Manual / UI Test** | Manually verify the page layout in a browser's responsive design mode. |

### 📁 Backend & Integration Tests

Tests for backend processes like logging and session management.

| Test Case ID | Request Name / Objective                                | Type                          | Key Checks / Notes                                                 |
| :----------- | :------------------------------------------------------ | :---------------------------- | :----------------------------------------------------------------- |
| `C14 / TC14` | Verify audit log entry after login attempt              | **Not Automatable (White-Box)** | Placeholder. Requires backend access to query logs or a database to verify. |
| `C15 / TC15` | Verify session management after successful login        | API (Stateful)                | **Requires Collection Runner.** Logs in, saves the `customerId`, and uses it to access a protected endpoint (`/accounts`). |

## Collection Variables

| Variable       | Purpose                                                                |
| :------------- | :--------------------------------------------------------------------- |
| `baseUrl`      | The base URL for the ParaBank API endpoint.                            |
| `customerId`   | Stores the customer ID after a successful login. It is set dynamically and used by subsequent requests to test session-dependent functionality. |


# ParaBank Login API Test Suite (JMeter)

This repository contains a comprehensive Apache JMeter test plan (`.jmx`) for testing the login functionality of the ParaBank application. The plan is a direct conversion of the scenarios outlined in the "ParaBank Login Test Suite" Postman collection, covering functional, security, and integration API tests.

## Overview

This test plan automates the process of validating the ParaBank REST API's login endpoint. It is designed for QA professionals to quickly assess the core login behavior, check for common security vulnerabilities, and verify backend session management.

### Key Features

*   **Comprehensive Coverage:** Includes positive, negative, and edge-case scenarios for the login process.
*   **Mirrors Postman Collection:** The test plan is structured with `Transaction Controllers` to logically group tests into Functional, Security, and Integration suites, matching the original collection's design.
*   **Dynamic Data Handling:** Automatically extracts the `customerId` from a successful login response and reuses it in subsequent requests to test authenticated endpoints (session management).
*   **Clear Assertions:** Every request includes `Response Assertions` to validate status codes and response body content, ensuring each test has a clear pass/fail condition.
*   **Easy Configuration:** Uses an `HTTP Request Defaults` element to manage the base URL, making it simple to retarget the tests to different environments (e.g., local, staging, production).

## Test Scenarios Included

The following automated API test scenarios are included in this plan:

###  Functional Tests
*   **C1 / TC01:** Login with valid username and password.
*   **C2 / TC02:** Login with valid username and invalid password.
*   **C3 / TC03:** Login with invalid username and valid password.
*   **C4 / TC04:** Attempt login with empty username and password fields.
*   **C5 / TC05:** Attempt login with whitespace-only username and password.

### Security Tests
*   **C8 / TC08:** Attempt login with a common SQL Injection payload (`' OR 1=1--`).
*   **C9 / TC09:** Attempt login with a common XSS payload (`<script>alert('XSS')</script>`).
*   **C10 / TC13:** Simulate multiple failed login attempts.
    *   *Note: This is a conceptual test to demonstrate the sequence. Actual account lockout depends on server-side configuration, which may not be active on the public ParaBank instance.*

### Backend & Integration Tests
*   **C15 / TC15:** Verify session management with a two-step process:
    1.  Perform a successful login and extract the `customerId`.
    2.  Use the extracted `customerId` to request a protected resource (`/customers/{customerId}/accounts`), verifying the session is valid.

---

## Excluded Scenarios (Manual/UI Tests)

The following scenarios from the original Postman collection are designed for manual UI testing and **cannot be automated via an API testing tool** like JMeter. They have been intentionally excluded from this test plan.

*   **C7 / TC07: Click “Register” link** (UI navigation)
*   **C11 / TC10: Verify password masking** (Front-end HTML property)
*   **C12 / TC11: Navigate form using only keyboard** (Browser accessibility)
*   **C13 / TC12: Responsive design on mobile device** (CSS rendering)
*   **C14 / TC14: Verify audit log entry** (Requires direct backend/database access)

---

## How to Use

1.  **Prerequisites:** Ensure you have the latest version of [Apache JMeter](https://jmeter.apache.org/download_jmeter.cgi) installed.
2.  **Open the Plan:** Launch JMeter and open the `ParaBank_Login_Suite.jmx` file via `File > Open`.
3.  **Run the Test:** Click the green "Start" button (play icon) in the toolbar to execute all scenarios.
4.  **Analyze Results:** Use the built-in **View Results Tree** and **Summary Report** listeners to see the outcome of each test. Green icons indicate a pass, while red icons indicate a failure. Click on any failed request to inspect the assertion results.

## JMeter Plan Structure

This plan utilizes several key JMeter components to replicate the Postman collection's logic:

| Feature | JMeter Implementation | Description |
| :--- | :--- | :--- |
| **Base URL Configuration** | `HTTP Request Defaults` | Sets the base URL (`https://parabank.parasoft.com`) for all requests. |
| **API Requests** | `HTTP Request Sampler` | Represents each individual API call to a specific endpoint. |
| **Test Validation** | `Response Assertion` | Checks the response code and body content for expected values. |
| **Variable Extraction** | `XPath Extractor` | Parses the XML response from a successful login to capture the `customerId`. |
| **Variable Usage** | `${customerId}` | Injects the captured customer ID into subsequent request paths. |
| **Logical Grouping** | `Transaction Controller` | Groups related samplers to organize the test plan and reports. |
