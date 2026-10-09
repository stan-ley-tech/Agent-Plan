# Checklist: Security

Apply only the sections relevant to the application and its risk profile. Mark items N/A with a reason. Passing this checklist does not mean the application is secure.

## Context

- [ ] Assets, their sensitivity, and the deployment context are identified.
- [ ] Trust boundaries and entry points are listed.

## Authentication

- [ ] Uses an established library or platform service; no custom crypto or password handling.
- [ ] Credentials are hashed with a current, appropriate algorithm (handled by the library).
- [ ] Session or token expiry, revocation, and secure cookie attributes are configured.
- [ ] Brute-force and credential-stuffing protections exist where the risk warrants.

## Authorization

- [ ] Every protected operation checks permission on the server.
- [ ] Access is checked per resource (ownership / tenant), not only per route.
- [ ] Default is deny; new endpoints are protected unless explicitly public.
- [ ] Administrative functions are separately protected.

## Input and output

- [ ] Input is validated at trust boundaries (type, length, format, range).
- [ ] Queries, commands, and paths use parameterized or safe APIs.
- [ ] Output is encoded for its context.
- [ ] File uploads are validated by content and size and stored safely.

## Data exposure

- [ ] Responses return only the fields the caller needs.
- [ ] Sensitive data is excluded from logs, error messages, and analytics.
- [ ] Data is encrypted in transit; at rest where sensitivity requires.
- [ ] Retention and deletion are defined for sensitive data.

## Secrets

- [ ] No secrets in code, configuration files, tests, documentation, or history.
- [ ] Secrets are loaded from the environment or a secret manager.
- [ ] Any exposed secret has been reported for rotation.

## Dependencies

- [ ] Audit tool run if available; actual results recorded.
- [ ] Vulnerable dependencies assessed for reachability and prioritized.
- [ ] Versions are locked.

## Configuration

- [ ] Debug and verbose error modes off outside development.
- [ ] CORS, security headers, and cookie settings are deliberate.
- [ ] No default credentials or exposed admin interfaces.

## Abuse and operations

- [ ] Abuse cases considered (enumeration, scraping, resource exhaustion, business-logic abuse).
- [ ] Rate limiting where abuse is plausible.
- [ ] Security-relevant events are logged with actor, action, target, and time.
- [ ] Least privilege applied to service accounts, database roles, and CI tokens.
