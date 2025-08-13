# ParaBank QA Automation: Customer Login Feature

This repository contains the Quality Assurance documentation for the **Customer Login** feature of the ParaBank application. It includes the Software Test Plan (STP) and the Functional Requirements Document (FRD) that guide the testing efforts.

## Project Details

| **Attribute**        | **Details**              |
| -------------------- | ------------------------ |
| **Project**          | ParaBank QA Automation   |
| **Feature**          | Customer Login           |
| **Author**           | Baseeil Elwali           |
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
    *   [11. Approval](#11-approval)
*   [Functional Requirements Document (FRD)](#functional-requirements-document-frd)
    *   [1. Feature Overview](#1-feature-overview)
    *   [2. Objectives](#2-objectives)
    *   [3. Functional Requirements](#3-functional-requirements)
    *   [4. Test Cases](#4-test-cases)
    *   [5. Security Considerations](#5-security-considerations)
    *   [6. Dependencies](#6-dependencies)

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

### 11. Approval
Prepared By: ___________________ Date: ___________
Reviewed By: ___________________ Date: ___________
Approved By: ___________________ Date: ___________


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
