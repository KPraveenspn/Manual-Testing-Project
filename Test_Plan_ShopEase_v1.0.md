# Test Plan Document
## ShopEase eCommerce Web Application
### Release v2.3.0 — Sprint 4

---

| Field | Details |
|---|---|
| **Document Title** | Test Plan — ShopEase eCommerce Platform |
| **Document Version** | v1.0 |
| **Project Name** | ShopEase Web Application — Release v2.3.0 |
| **Prepared By** | [Your Name], Senior QA Engineer |
| **Reviewed By** | [QA Manager Name], QA Lead |
| **Approved By** | [Product Owner Name], Product Owner |
| **Date Created** | 01 June 2026 |
| **Last Updated** | 10 June 2026 |
| **Status** | Approved |

---

## Table of Contents

1. [Project Introduction](#1-project-introduction)
2. [Objectives](#2-objectives)
3. [Scope](#3-scope)
4. [Test Strategy](#4-test-strategy)
5. [Test Levels](#5-test-levels)
6. [Test Types](#6-test-types)
7. [Entry Criteria](#7-entry-criteria)
8. [Exit Criteria](#8-exit-criteria)
9. [Test Environment](#9-test-environment)
10. [Risks and Mitigations](#10-risks-and-mitigations)
11. [Deliverables](#11-deliverables)
12. [Roles and Responsibilities](#12-roles-and-responsibilities)
13. [Test Schedule](#13-test-schedule)
14. [Assumptions](#14-assumptions)

---

## 1. Project Introduction

### 1.1 Application Overview

**ShopEase** is a B2C eCommerce web platform that enables customers to browse products, manage a shopping cart, and complete purchases through an integrated payment gateway. The platform supports guest and registered user journeys and offers advanced search, filtering, and personalised recommendation features.

**Technology Stack:**
- **Frontend:** React.js 18, Tailwind CSS
- **Backend:** Node.js + Express REST API
- **Database:** PostgreSQL 14
- **Payment Gateway:** Stripe v3
- **Hosting:** AWS (EC2, S3, CloudFront)
- **CDN:** AWS CloudFront

### 1.2 Release Context

Release v2.3.0 introduces the following changes:
- Redesigned Product Detail Page (PDP) with image zoom and variant selector
- Revamped Checkout flow with address auto-fill via Google Places API
- New promo code / coupon engine integrated with cart
- Bug fixes from v2.2.1 (12 defects resolved)
- Performance optimisations on search and filtering

### 1.3 Business Criticality

ShopEase processes an average of **1,200 orders per day**, with peak transactions during promotional events reaching up to **4,500 orders/day**. Any defect in the checkout or payment flow carries high financial risk and requires zero-tolerance quality thresholds.

---

## 2. Objectives

The primary objectives of this test plan are:

1. Validate that all newly developed and modified features in v2.3.0 function as per the Business Requirements Specification (BRS) and Functional Specification Document (FSD).
2. Ensure no regression has been introduced into existing stable functionality.
3. Verify that the application is accessible, responsive, and performant across targeted browsers and devices.
4. Identify, document, and track all defects prior to production deployment.
5. Provide a formal QA sign-off and release readiness recommendation to the Product and Engineering teams.
6. Achieve a minimum **pass rate of 90%** on all high-priority test cases before release approval.

---

## 3. Scope

### 3.1 In Scope

| Module | Features / User Stories |
|---|---|
| **Authentication** | User registration, login (email/password), logout, forgot password / reset password flow, session management, remember-me functionality |
| **Homepage** | Banner carousel, navigation menu, category shortcut tiles, featured products section, search bar |
| **Product Listing Page (PLP)** | Product grid, pagination, sorting (price, rating, newest), filtering (category, brand, price range, rating) |
| **Product Detail Page (PDP)** | Image gallery, zoom, variant selection (size/colour), stock indicator, add-to-cart, add-to-wishlist |
| **Search** | Keyword search, autocomplete suggestions, zero-results handling, search result relevance |
| **Shopping Cart** | Add items, remove items, update quantity, price calculation, promo code application, cart persistence |
| **Checkout** | Guest checkout, address entry and validation, shipping method selection, order summary review |
| **Payment** | Card payment via Stripe, invalid card handling, 3DS authentication simulation, order confirmation |
| **Form Validation** | All input fields — mandatory field checks, format validation, error message accuracy |
| **Responsive / Cross-Browser** | Desktop (1920×1080, 1366×768), tablet (768×1024), mobile (375×667, 390×844) |

### 3.2 Out of Scope

The following areas are **explicitly excluded** from this test cycle:

- Admin / Back-Office Panel (separate test cycle)
- API Performance / Load / Stress Testing (handled by Performance Engineering team)
- Native iOS and Android mobile applications
- Third-party seller onboarding module
- Email / SMS notification delivery testing (covered by integration team)
- Accessibility (WCAG 2.1) compliance audit (scheduled for Q3)
- Database integrity testing beyond UI-level data validation

---

## 4. Test Strategy

### 4.1 Approach

Testing will follow a **risk-based testing** approach. Test effort will be prioritised according to business impact and defect probability. High-risk, high-impact modules (Checkout, Payment, Authentication) receive maximum coverage and will be tested first.

**Techniques applied:**
- **Equivalence Partitioning (EP):** Grouping valid and invalid input classes
- **Boundary Value Analysis (BVA):** Testing minimum, maximum, and edge values
- **Decision Table Testing:** For complex business rules (e.g., promo code eligibility)
- **State Transition Testing:** For cart item states and order status workflows
- **Exploratory Testing:** Ad-hoc sessions on each module after scripted execution

### 4.2 Test Prioritisation

| Priority Level | Criteria | Examples |
|---|---|---|
| **P1 — Critical** | Business-blocking; cannot release without fix | Login broken, payment failure, checkout crash |
| **P2 — High** | Major feature defect; significant user impact | Cart total miscalculation, forgot password not sending email |
| **P3 — Medium** | Functional defect with workaround available | Incorrect sort order, filter count inaccuracy |
| **P4 — Low** | Cosmetic / minor UX issues | Typos, minor alignment issues, tooltip text errors |

---

## 5. Test Levels

### 5.1 System Testing
Comprehensive black-box testing of the fully integrated ShopEase application. All test cases in this document operate at the system level, simulating real end-user behaviour through the browser UI.

### 5.2 System Integration Testing (SIT)
Validation of integration points between ShopEase and third-party services:
- **Stripe Payment Gateway** — Payment authorisation, decline handling
- **Google Places API** — Address autocomplete in checkout
- **SendGrid** — Email trigger verification (password reset, order confirmation)

### 5.3 Regression Testing
Full regression suite execution on all previously passing test cases following any defect fix deployment to the UAT environment. Regression is triggered before every release candidate build.

### 5.4 User Acceptance Testing (UAT)
Facilitated session with Product Owner and business stakeholders in the UAT environment. QA team provides test scripts and observational support. UAT sign-off is a prerequisite for production deployment.

---

## 6. Test Types

| Test Type | Description | Responsibility |
|---|---|---|
| **Functional Testing** | Validate all features against acceptance criteria | QA Engineer |
| **Negative Testing** | Validate system behaviour with invalid/unexpected inputs | QA Engineer |
| **UI / Usability Testing** | Verify visual layout, element alignment, font consistency, colour contrast | QA Engineer |
| **Regression Testing** | Ensure no new defects introduced by recent code changes | QA Engineer |
| **Smoke Testing** | Quick sanity check post-deployment to verify environment stability | QA Engineer |
| **Cross-Browser Testing** | Execute critical paths on Chrome, Firefox, Safari, Edge | QA Engineer |
| **Responsive Testing** | Verify layout integrity on desktop, tablet, and mobile viewports | QA Engineer |
| **Exploratory Testing** | Unscripted investigation of high-risk areas | QA Engineer |
| **End-to-End Testing** | Full user journey: registration → search → cart → checkout → confirmation | QA Engineer |

---

## 7. Entry Criteria

The following conditions **must be met** before test execution commences:

- [ ] Release v2.3.0 build has been deployed to the **UAT/Staging environment**
- [ ] Smoke test on the build passes (critical paths accessible)
- [ ] All required test data (user accounts, product catalogue, test cards) is provisioned
- [ ] Business Requirements Specification (BRS) and FSD are approved and baselined
- [ ] All P1 defects from the previous cycle are closed or accepted as known issues
- [ ] Test environment configuration is verified and signed off by DevOps
- [ ] TestRail test suite is set up and all test cases are reviewed and approved
- [ ] QA team has been onboarded to the UAT environment with correct access credentials

---

## 8. Exit Criteria

Test execution is considered **complete** when:

- [ ] 100% of written test cases have been executed
- [ ] A minimum **pass rate of 90%** is achieved on P1 and P2 test cases
- [ ] All **Critical (P1)** defects are resolved and re-tested as PASS
- [ ] All **High (P2)** defects are either resolved or formally accepted by the Product Owner with documented risk
- [ ] Test Summary Report is prepared, reviewed, and approved
- [ ] QA Sign-Off is obtained from the QA Lead / Manager
- [ ] UAT sign-off is obtained from the Product Owner

**Note:** Release may proceed with known P3 and P4 defects if formally accepted in the risk register.

---

## 9. Test Environment

### 9.1 Environments

| Environment | URL | Purpose |
|---|---|---|
| **Development** | https://dev.shopease.internal | Developer unit testing |
| **Staging / UAT** | https://staging.shopease.com | QA and UAT testing |
| **Production** | https://www.shopease.com | Live environment (no testing) |

### 9.2 Browser & Device Matrix

| Browser / Device | Version | Platform | Priority |
|---|---|---|---|
| Google Chrome | Latest (stable) | Windows 11 | P1 |
| Mozilla Firefox | Latest (stable) | Windows 11 | P1 |
| Safari | 17.x | macOS Ventura | P1 |
| Microsoft Edge | Latest (stable) | Windows 11 | P2 |
| Chrome (Mobile) | Latest | iPhone 14 Pro (iOS 17) | P1 |
| Safari (Mobile) | 17.x | iPhone 14 Pro (iOS 17) | P1 |
| Chrome (Mobile) | Latest | Samsung Galaxy S23 (Android 14) | P2 |

### 9.3 Test Data Requirements

| Data Type | Details |
|---|---|
| **Registered User** | testuser@shopease.com / Password123! |
| **New User (Registration)** | qa.newuser+[timestamp]@shopease.com |
| **Invalid User** | invalid@noexist.com / WrongPass99 |
| **Test Products** | Pre-seeded: 50 products across 5 categories |
| **Test Payment Card (Stripe)** | 4242 4242 4242 4242 | Exp: 12/27 | CVV: 123 |
| **Declined Card (Stripe)** | 4000 0000 0000 0002 | Exp: 12/27 | CVV: 123 |
| **3DS Card (Stripe)** | 4000 0025 0000 3155 | Exp: 12/27 | CVV: 123 |
| **Promo Code** | SAVE10 (10% off), FREESHIP (free shipping) |

---

## 10. Risks and Mitigations

| # | Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|---|
| R01 | Staging environment instability causing false failures | Medium | High | Coordinate with DevOps for environment health monitoring; maintain test execution log with timestamps |
| R02 | Test data reset wiping user accounts or product catalogue between executions | Medium | High | Automate test data seeding via setup scripts; document data dependencies |
| R03 | Stripe sandbox API downtime blocking payment test cases | Low | Critical | Schedule payment testing during Stripe's published high-availability windows; maintain offline test evidence for known-good flows |
| R04 | Incomplete or ambiguous requirements causing test gaps | Medium | High | Conduct requirement review meetings; raise ambiguity as QA queries in JIRA before test design |
| R05 | Late code delivery compressing the test execution window | High | High | Prioritise P1/P2 test cases in first execution cycle; prepare risk-based release recommendation |
| R06 | Key QA resource unavailability | Low | Medium | Ensure test case documentation is sufficient for a secondary QA engineer to execute |
| R07 | Cross-browser CSS defects not caught until late in cycle | Medium | Medium | Integrate cross-browser checks into daily exploratory sessions from Day 1 |

---

## 11. Deliverables

| # | Deliverable | Owner | Target Date |
|---|---|---|---|
| D01 | Test Plan Document (this document) | QA Engineer | 02 Jun 2026 |
| D02 | Test Cases — All Modules | QA Engineer | 04 Jun 2026 |
| D03 | Defect Reports (JIRA) | QA Engineer | Ongoing |
| D04 | Daily Test Execution Status Update | QA Engineer | Daily |
| D05 | Test Summary Report | QA Engineer | 13 Jun 2026 |
| D06 | QA Sign-Off Memo | QA Lead | 14 Jun 2026 |
| D07 | UAT Test Scripts for Stakeholders | QA Engineer | 10 Jun 2026 |

---

## 12. Roles and Responsibilities

| Role | Name | Responsibilities |
|---|---|---|
| **QA Engineer (Lead)** | [Your Name] | Test planning, test case design, execution, defect reporting, summary reporting |
| **QA Manager** | [Manager Name] | Test plan review/approval, escalation management, QA sign-off |
| **Product Owner** | [PO Name] | Requirements clarification, UAT facilitation, release approval |
| **Dev Lead** | [Dev Lead Name] | Defect fix, code deployment to staging, fix verification support |
| **DevOps Engineer** | [DevOps Name] | Environment provisioning, deployment pipeline, test data seeding |
| **Business Analyst** | [BA Name] | Requirements documentation, ambiguity resolution |

---

## 13. Test Schedule

| Phase | Activity | Start Date | End Date | Duration |
|---|---|---|---|---|
| **Phase 1** | Test Planning & Review | 01 Jun 2026 | 02 Jun 2026 | 2 days |
| **Phase 2** | Test Case Design & Review | 03 Jun 2026 | 04 Jun 2026 | 2 days |
| **Phase 3** | Test Environment Setup & Smoke Test | 05 Jun 2026 | 05 Jun 2026 | 1 day |
| **Phase 4** | Test Execution — Cycle 1 | 06 Jun 2026 | 10 Jun 2026 | 5 days |
| **Phase 5** | Defect Fix & Re-test | 11 Jun 2026 | 12 Jun 2026 | 2 days |
| **Phase 6** | Regression Testing | 12 Jun 2026 | 12 Jun 2026 | 1 day |
| **Phase 7** | UAT Support | 13 Jun 2026 | 13 Jun 2026 | 1 day |
| **Phase 8** | Test Closure & Reporting | 14 Jun 2026 | 15 Jun 2026 | 1 day |
| **Total** | | **01 Jun 2026** | **15 Jun 2026** | **15 days** |

---

## 14. Assumptions

1. The BRS and FSD are stable and approved before test execution begins. Any mid-cycle changes require a formal change request and impact assessment.
2. The staging environment mirrors the production infrastructure with equivalent data volumes.
3. Test data will be provisioned and reset by the DevOps team at the start of each execution cycle.
4. The development team will adhere to a minimum **24-hour turnaround** for P1 defect fixes during the execution phase.
5. QA team will have full access to JIRA, TestRail, BrowserStack, and the staging environment from Day 1.
6. Stripe sandbox environment will be available and functioning throughout the test cycle.
7. All team members will attend the daily stand-up for status updates and blocker resolution.
8. Any defects identified in out-of-scope areas will be logged in JIRA for the next release cycle.

---

**Document History**

| Version | Date | Author | Changes |
|---|---|---|---|
| v0.1 | 01 Jun 2026 | [Your Name] | Initial draft |
| v0.2 | 02 Jun 2026 | [Your Name] | Added risk register, test data section |
| v1.0 | 02 Jun 2026 | [QA Manager] | Reviewed and approved |

---

*This document is version-controlled. Any changes after approval must go through a formal change management process and require re-approval by the QA Manager and Product Owner.*
