# Findings Analysis

This document summarizes the evidence, logic, and risk framing behind the main observations in this project. The purpose is not to assert final exploitation but to identify control gaps and support a business-based remediation plan.

## F01 — Potential remote file inclusion

**Evidence basis:** Nikto flags a potential file parameter issue. This is an investigation item, not confirmed exploitation.

**Observation:** A parameter appears to allow selection of a remote or external resource path. That creates a potential file inclusion condition if the application consumes the value without safe validation.

**Business consequence:** If confirmed, an attacker could influence application behavior and potentially expose or execute unauthorized content.

**Recommended treatment:** Validate the code path in a lab environment, restrict file selection to approved values, and remove any remote inclusion functionality.

## F02 — Anonymous FTP login

**Evidence basis:** OpenVAS reference material reports anonymous FTP access.

**Observation:** The evidence suggests a service is permitting unauthenticated access to file content or a login capability without a valid user context.

**Business consequence:** Unauthorized users could access filesystem content or reconnaissance material if sensitive files are available.

**Recommended treatment:** Disable anonymous access unless the business has an explicit and approved public-distribution requirement.

## F03 — Exposed phpinfo endpoint

**Evidence basis:** Scanner output and user screenshot corroborate an exposed diagnostic page.

**Observation:** A phpinfo endpoint is reachable and reveals detailed configuration data that should not be available to general users.

**Business consequence:** Attackers may use the information to identify vulnerable components, configurations, or deployment assumptions.

**Recommended treatment:** Remove the endpoint from production deployments or restrict access to authorized administrators.

## F04 — PHPSESSID without HttpOnly

**Evidence basis:** Nikto reports a session cookie without HttpOnly.

**Observation:** The application may allow JavaScript access to the session cookie, increasing risk if script execution occurs elsewhere.

**Business consequence:** Session theft or abuse becomes more likely if a separate script injection issue is present.

**Recommended treatment:** Set HttpOnly on the session cookie and review the broader cookie policy including Secure and SameSite settings.

## F05 — Directory listing enabled

**Evidence basis:** Nikto output references a directory listing in a public path.

**Observation:** Content in the directory may be exposed without authentication or user approval.

**Business consequence:** The issue may reveal internal content, metadata, or support files that reduce system confidentiality.

**Recommended treatment:** Disable directory indexing and inventory exposed files.

## F06 — Apache /server-status exposed

**Evidence basis:** Nikto identifies an exposed status endpoint.

**Observation:** Operational telemetry or server details are available to users who should not have that access.

**Business consequence:** The disclosure supports reconnaissance and can provide attacker context about the system environment.

**Recommended treatment:** Restrict access to the status endpoint and verify its business necessity.

## F07 — Clickjacking protection absent or incomplete

**Evidence basis:** Scanner output suggests missing framing protections.

**Observation:** The application may not provide adequate protection against embedding in another site.

**Business consequence:** Sensitive actions can be framed or manipulated if users interact with the application from a malicious page.

**Recommended treatment:** Configure appropriate frame protections, such as X-Frame-Options or Content Security Policy frame-ancestors.

## F08 — DEBUG HTTP method enabled

**Evidence basis:** Nikto flags a DEBUG method as potentially exposing diagnostics.

**Observation:** A diagnostic method may be enabled on the application-facing web service.

**Business consequence:** Debug information exposure could reveal configuration details or application internals.

**Recommended treatment:** Validate the actual behavior and disable the method if not required.

## F09 — ICMP timestamp disclosure

**Evidence basis:** Published OpenVAS reference reports ICMP timestamp disclosure.

**Observation:** The network service may respond to timestamp requests and disclose reconnaissance information.

**Business consequence:** This is lower priority than access and data exposure issues, but it still reduces confidentiality and supports operational profiling.

**Recommended treatment:** Restrict timestamp responses if they are not required for normal network operations.

## Priority and governance stance

The project uses a validation-first posture. The most important items are those that could create direct compromise or unauthorized access. Lower-priority findings should still be tracked, but they should not distract from the risks that create actual business exposure.

This document is intended to support the executive memo and the POA&M workbook while preserving the evidence trail used during the assessment.
