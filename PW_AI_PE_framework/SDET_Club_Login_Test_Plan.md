# Test Plan: SDET Club Login

## 1. Test Plan ID and Title

| Field | Value |
| --- | --- |
| Test Plan ID | TP-SDET-LOGIN-001 (locally assigned) |
| Title | SDET Club Hosted Login Functional Test Plan |
| Status | Draft for review |
| Application | SDET Club, sign-in hosted by Circle |
| Feature | Email and password login |

## 2. Objective and References

### Objective

Define a reproducible functional test approach for successful login and rejection of invalid or missing credentials. The plan is based on the supplied expected behavior and does not claim that any test has been executed.

### References and evidence

| Reference | What it establishes |
| --- | --- |
| User-provided URL: https://www.sdetclub.com/c/playwright-4x | Entry point supplied for the target; it redirected to the hosted sign-in page during inspection. |
| Hosted sign-in: https://login.circle.so/sign_in?request_host=www.sdetclub.com#email | Visible controls observed: Email, Password, Sign In, and Forgot your password? This inspection did not verify login outcomes. |
| User-provided expected behavior | Valid credentials should log in and show a successful-login message. Wrong user ID/email or password should prevent login. |

The exact success message, invalid-login feedback, and post-login destination have not been supplied or verified. Confirm these before execution.

## 3. In Scope and Out of Scope

### In scope

- Functional login using valid credentials.
- Rejection of an incorrect email/user ID and, separately, an incorrect password.
- Required-field behavior for a blank email, a blank password, and both fields blank.
- Observable authenticated versus unauthenticated state after submission.

### Out of scope

- Password reset, account creation, MFA, SSO, or social login.
- Account lockout policy, security penetration testing, performance, and load testing.
- Broader Playwright course content or testing of unrelated SDET Club features.

## 4. Requirements and Planned Coverage

The requirement IDs below are local identifiers assigned for this plan; no external requirement IDs were provided.

| Requirement ID | Requirement | Planned coverage | Expected result basis |
| --- | --- | --- | --- |
| REQ-LOGIN-01 (local) | A user with valid credentials can log in. | Submit valid test-account credentials. | User reaches an authenticated state and the agreed successful-login message is visible. Exact message and destination are to be confirmed. |
| REQ-LOGIN-02 (local) | An incorrect email/user ID does not authenticate the user. | Submit a non-existent or otherwise approved invalid account identifier with a password. | Login is denied and the user remains unauthenticated. Exact feedback is to be confirmed. |
| REQ-LOGIN-03 (local) | An incorrect password does not authenticate the user. | Submit the approved test account identifier with an incorrect password. | Login is denied and the user remains unauthenticated. Exact feedback is to be confirmed. |
| REQ-LOGIN-04 (local) | Email is required for login. | Submit with the email field blank and password populated. | Login is not completed; exact validation behavior is to be confirmed. |
| REQ-LOGIN-05 (local) | Password is required for login. | Submit with the password field blank and email populated. | Login is not completed; exact validation behavior is to be confirmed. |
| REQ-LOGIN-06 (local) | Both required credentials are needed for login. | Submit with both fields blank. | Login is not completed; exact validation behavior is to be confirmed. |

## 5. Test Approach, Levels, and Types

### Approach

- Perform UI-level functional testing of the hosted sign-in form.
- Cover one positive scenario and five negative scenarios mapped to REQ-LOGIN-01 through REQ-LOGIN-06.
- Verify authentication state and visible feedback, using agreed application evidence rather than assuming specific message text.
- Use Playwright for browser automation as a proposed approach; the framework version and implementation details are not yet agreed.
- Treat this plan as test design only. No scripts have been generated and no tests have been run.

### Levels and types

| Level/type | Application to this plan |
| --- | --- |
| System/UI functional | Primary level: exercise the sign-in form and observe resulting state. |
| Positive testing | Confirm valid credentials produce the agreed successful-login state. |
| Negative testing | Confirm wrong or missing credentials do not authenticate. |
| Regression smoke | Re-run the six planned scenarios after relevant sign-in changes; wider regression is outside this plan. |
| Compatibility | Browser coverage is pending agreement; Chromium is a proposed initial baseline only. |

API, security, performance, and load testing are excluded from this plan.

## 6. Environment, Tools, Access, and Test Data

| Item | Current plan / status |
| --- | --- |
| Target | Supplied SDET Club course URL, which redirects to Circle's hosted sign-in page. User confirmed this hosted target is authorized for testing; no separate URL was provided. |
| Access | User reports an approved test account is available. Credentials must be retrieved through the approved secret mechanism and must not be placed in this plan or source control. |
| Visible controls | Email, Password, Sign In, and Forgot your password? observed on the hosted page. |
| Test tool | Playwright is proposed based on the supplied course context; exact version and runner configuration are Not provided. |
| Browser / OS / device | Not provided. Chromium on desktop is a proposed initial target, pending agreement; add other browsers/devices only when the matrix is confirmed. |
| Positive data | Active, authorized test account with valid credentials; account state and access prerequisites to be confirmed before execution. |
| Negative data | Approved invalid account identifier and incorrect password; use synthetic values where possible. Do not use real user credentials. |
| Blank-field data | Empty email and/or password values for the three required-field scenarios. |
| Expected-state oracle | Exact success message, destination, invalid-credential feedback, and required-field validation are Not provided and must be confirmed before execution. |

## 7. Entry and Exit Criteria

### Entry criteria

- The authorized hosted target is reachable and the approved test account can be used for this test activity.
- Expected success message, authenticated-state evidence, and invalid/blank-field outcomes are confirmed by the product owner or application owner.
- The browser, operating system, and Playwright version for execution are agreed.
- Test data is available through an approved non-secret mechanism, and any account reset or cleanup procedure is documented.
- No known environment outage or access restriction prevents safe test execution.

### Exit criteria (proposed; requires agreement)

- All six planned scenarios have an execution result and recorded evidence or a documented reason they could not run.
- Every executed scenario passes, or each failure has a linked defect with severity, owner, and disposition.
- No unresolved blocker or critical authentication defect remains; severity definitions and any accepted exceptions are agreed during triage.
- Results are reviewed against the confirmed expected outcomes. These criteria describe a proposed gate, not completed verification.

## 8. Roles, Responsibilities, Estimates, and Schedule

| Role | Responsibility | Assignment |
| --- | --- | --- |
| QA/SDET | Prepare and execute the approved scenarios, retain evidence, and report defects. | Not provided |
| Product/application owner | Confirm success and failure behavior, approve the browser matrix, and review results. | Not provided |
| Test-account owner | Provision or validate the approved account and confirm reset/cleanup needs. | Not provided |
| Development/support contact | Triage authentication defects and advise on service incidents. | Not provided |

Effort estimates and schedule are Not provided. Estimate after the expected outcomes, browser matrix, tool version, and ownership are confirmed.

## 9. Defect Management and Reporting

- Record each defect with a concise title, environment/browser, preconditions, sanitized test data, reproducible steps, expected and actual results, timestamp, evidence, and linked local requirement ID.
- Do not attach passwords, session tokens, or other secrets to defect records or logs.
- Use the team's existing defect tracker; tool and workflow are Not provided.
- Proposed severity: Blocker/Critical for a broad inability to authenticate or an authentication bypass; Major for a scoped failure of an agreed login scenario; Minor for non-blocking usability or validation feedback. Confirm the team's severity definitions before execution.
- Triage failures with QA, the application owner, and development/support. Escalate suspected authentication bypasses or exposure immediately through the approved security incident process.
- Proposed reporting cadence: summarize results after each execution cycle and report blockers or suspected security issues immediately. Named owner and recipient list are Not provided.

## 10. Risks, Dependencies, Assumptions, and Open Questions

### Risks and dependencies

- The sign-in is hosted by Circle and may change independently of the SDET Club course page; verify the target and visible controls before each run.
- Repeated invalid attempts may trigger rate limiting or account protection. Keep execution to the approved cases and stop if a lockout, challenge, or unexpected security control appears.
- A valid account and approved secret-handling method are required. The user reports an approved test account is available; access details are intentionally not included here.
- Playwright, browser, operating system, and defect tracker versions/tools remain to be agreed.

### Assumptions

- The supplied hosted sign-in is the authorized test target, as confirmed by the user.
- The approved test account can be used for the planned functional scenarios.
- Requirement IDs in this plan are local traceability IDs, not external system identifiers.

### Open questions before execution

- What exact success message and authenticated destination/state should be asserted?
- What visible feedback or validation behavior is expected for incorrect and blank credentials?
- Which browser(s), operating system(s), and Playwright version are in scope?
- Who approves the acceptance oracle, owns the test account, executes the cases, and reviews results?
- Which defect tracker, severity convention, and reporting recipients should be used?

## 11. Suspension and Resumption Criteria

### Suspend testing when

- The hosted sign-in is unavailable, materially changed, or redirects to an unexpected destination.
- The approved test account is locked, challenged, or otherwise unavailable, or repeated attempts appear to trigger protection controls.
- The expected authenticated/unauthenticated state cannot be determined reliably.
- A suspected authentication bypass, sensitive-data exposure, or other security concern is observed; stop and use the approved incident process.
- Continuing could affect a real user, account, or service beyond the approved test scope.

### Resume testing when

- The target and required sign-in behavior are confirmed, and the service is available.
- Account access and safe test data are restored through the approved process.
- The application owner/QA lead has reviewed any incident or blocker and explicitly approved resumption.
- The remaining scenarios and any required cleanup are agreed and documented.

## 12. Test Deliverables and Approval

### Deliverables

- This login test plan and its requirement-to-coverage mapping.
- After separate execution approval: scenario-level results, sanitized evidence, and linked defect records, if any.
- Automation scripts, detailed test cases, and execution reports are not included in this plan artifact.

### Approval

| Approval role | Name / status |
| --- | --- |
| QA/SDET reviewer | Not provided |
| Product/application owner | Not provided |
| Approval status | Draft; approval pending |

Approval of this plan does not constitute execution approval beyond the user's stated authorization for the target. Confirm the listed open questions and any organizational release gates before running tests.