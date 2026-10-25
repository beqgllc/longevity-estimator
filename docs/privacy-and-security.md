# Privacy and Security

## 1. Scope and risk profile

The application may collect sensitive information, including birth date, approximate location, demographic characteristics, medical diagnoses, mental-health conditions, medication use, substance-use history, smoking, housing, and functional status. The combination can be identifying even if a name is not requested.

Treat questionnaire payloads and derived model features as sensitive. Derived risk scores can reveal or infer sensitive facts and should receive equivalent protection.

This document is an engineering baseline, not a legal determination that a service is compliant with HIPAA, the FTC Act/Health Breach Notification Rule, state consumer-health privacy laws, or other laws. Applicability depends on the operator, product, users, data flows, contracts, and jurisdictions. Obtain qualified privacy and legal review before production use.

## 2. Data minimization and default behavior

- Do not require an account for an anonymous assessment.
- Do not persist raw answers by default.
- Keep data in session memory where feasible and clear it when the user resets or finishes according to the disclosed behavior.
- Make any local draft saving explicit and opt-in; explain device risks and how to erase it.
- Do not collect precise address, exact GPS, name, contact information, or clinical documents unless justified by a documented requirement.
- Make optional demographic and clinical fields genuinely optional.
- Do not turn declined/unknown fields into negative answers.
- Do not use answers for ads, employment screening, insurance eligibility, profiling, or unrelated secondary use.
- Do not send answers to external LLM, AI, analytics, crash-reporting, or advertising services by default.

## 3. Data flow inventory

Before deployment, maintain a current inventory describing:

| Data | Purpose | Processing location | Persisted? | Access | Retention/deletion |
|---|---|---|---|---|---|
| Questionnaire answers | Feature derivation and estimation | [Client/server] | [No by default] | [Roles] | [Policy] |
| Derived features | Validated model input | [Location] | [No by default] | [Roles] | [Policy] |
| Estimate and provenance | Display result and reproducibility | [Location] | [No by default] | [Roles] | [Policy] |
| Operational logs | Service health without content | [Location] | [Limited] | [Roles] | [Policy] |

Do not launch with undocumented data flows or placeholder retention terms.

## 4. Transport, storage, and secrets

- Use HTTPS in deployment and secure cookies if cookies are needed.
- Keep server secrets in the hosting platform's secret manager or server-only environment; never put secrets in `NEXT_PUBLIC_*` variables.
- Commit only `.env.example`, never real `.env` files.
- If data persistence is later introduced, define encryption at rest/in transit, key rotation, backup protection, role-based access, audit trails, deletion behavior, and incident response.
- Do not store raw answers in URL query parameters, browser history, logs, analytics, or referrer headers.
- Use parameterized database queries and a restrictive Content Security Policy where practical.
- Validate all server inputs even if the client validates them.
- Apply rate limits and abuse protections to server endpoints without logging sensitive payloads.

## 5. Logging and monitoring

Safe logs may include request ID, timestamp, route, latency, error class, model/version identifier, and non-sensitive operational metadata. Do not log raw question answers, dates of birth, postal codes, free-text medical descriptions, substance lists, medication names, or per-person risk results. Sanitize exception messages and third-party errors before logging.

If monitoring requires assessment records, pause and perform a separate privacy review instead of retaining them by default.

## 6. Third-party services

Maintain an inventory of hosting, model services, datasets, telemetry, monitoring, email, maps/geocoding, and other providers. Document data sent to each provider, purpose, retention, subprocessors, contractual safeguards, and opt-out behavior. Avoid external services that receive sensitive answers unless explicitly necessary, disclosed, reviewed, and lawfully configured.

## 7. User control and disclosures

Before collecting answers, provide a plain-language notice describing:

- what categories are collected;
- why each category is requested;
- which inputs are optional;
- how calculation occurs;
- which data are sent off-device, if any;
- whether anything is stored and for how long;
- how a user can erase saved data;
- the statistical limitations of the result;
- contact and privacy-request routes for deployed versions.

Provide a visible reset/clear action. Confirm what it clears; do not claim to delete remote records unless the implementation actually does so.

## 8. Special handling for high-risk disclosures

Mental-health and substance-use answers must be handled neutrally. The app is not a crisis service or a diagnostic tool. Do not imply that an answer proves immediate danger. If the app adds crisis detection or guidance, that feature must have its own clinically reviewed, location-aware safety design; do not infer emergency location or promise response by a clinician.

## 9. Access and repository security

- Grant GitHub Actions only the permissions required by each workflow.
- Pin actions to reviewed immutable commit SHAs for high-assurance deployments; automate and review updates.
- Enable dependency and secret scanning where available.
- Require review for changes to model coefficients, data imports, estimation calculations, and privacy controls.
- Keep raw assessment samples out of tests; use synthetic data.
- Protect default-branch rules and require CI checks before merging.
- Do not put actual customer or patient data in issues, pull requests, screenshots, or bug reports.

## 10. Incident response

Document an owner and a process to detect, contain, investigate, remediate, and notify affected parties where required after suspected disclosure, unauthorized access, data loss, or secret exposure. Revoke leaked credentials immediately. Do not delete audit evidence needed for a lawful incident investigation. Follow current legal and contractual requirements for notifications.

## 11. Pre-release checklist

- [ ] Data inventory completed and reviewed.
- [ ] No raw answers in logs, analytics, URLs, or external services.
- [ ] No persistence by default, or persistence separately reviewed and disclosed.
- [ ] Environment and secrets handling reviewed.
- [ ] User data reset/deletion behavior tested.
- [ ] Access control and rate limits reviewed.
- [ ] Dependencies and workflows audited.
- [ ] Privacy notice reviewed for actual product behavior.
- [ ] Relevant legal/compliance review completed.
- [ ] Incident response owner and process documented.
