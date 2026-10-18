---
name: web-security-checklist
description: Security review for AI-built websites and web apps before they go live. Use whenever a project has a backend, database, login, forms, API keys, paid APIs (AI calls), file uploads, or gets deployed/hosted publicly — and when the user asks for a security check, audit or "is this safe to put online".
---

# Web Security Checklist

AI-generated web apps tend to ship the same handful of holes. Go through every section that applies to this project, check the actual code and config (not assumptions), and report each item as PASS / FAIL / N/A with file:line for failures. Fix FAILs before calling the project done, unless the user says otherwise.

Skip sections that clearly don't apply (a static page with no forms and no keys only needs sections 1, 6 and 8). Say which you skipped.

## 1. Secrets

- No API keys, database URLs, service-role keys or tokens in frontend code, HTML, or anything bundled for the browser. Search the build output too, not only the source.
- Keys that must exist client-side (e.g. a public anon key) are the restricted, public kind — never admin/service keys.
- Secrets live in environment variables or a server-side config that is not committed. `.env` is in `.gitignore`.
- No secrets in git history, logs, error messages or screenshots.

## 2. Authentication and authorization

- Every non-public route and API endpoint checks that the user is logged in — on the server, not only by hiding buttons in the UI.
- Every request that reads or changes a record checks that this user owns it or is allowed to (no "change the ID in the URL and see someone else's data").
- Passwords are hashed with a slow algorithm (bcrypt, scrypt, argon2) — never stored plain or with a fast hash. Prefer an existing auth provider over hand-rolled auth.
- Sessions/tokens expire, cookies are `HttpOnly`, `Secure`, `SameSite=Lax` or stricter.

## 3. Database

- Database access rules are locked down: row-level security / security rules on, default deny, no "allow read, write: if true".
- Queries are parameterized or go through an ORM — no SQL built by string concatenation with user input.
- The database is not reachable from the internet unless it has to be.

## 4. Input and output

- All user input is validated on the server (type, length, allowed values) — client-side validation is only for UX.
- Output is escaped; no `innerHTML`/`dangerouslySetInnerHTML` with user content. If HTML must be rendered, it is sanitized with a maintained library.
- File uploads: type and size limits, stored outside the web root or in object storage, never executed.

## 5. Abuse and cost

- Rate limiting on login, sign-up, password reset, contact forms and every endpoint that is expensive.
- Any endpoint that calls a paid API (AI models, email, SMS) is behind auth or strict rate limits, and the paid account has a hard spending cap set at the provider.
- Forms that send email have spam protection.

## 6. Transport and headers

- HTTPS everywhere, HTTP redirects to HTTPS.
- CORS allows only the origins that need it — no `*` together with credentials.
- Basic security headers set: `Content-Security-Policy` (at least a sane default), `X-Content-Type-Options: nosniff`, `Referrer-Policy`, `frame-ancestors`/`X-Frame-Options`.

## 7. Dependencies and errors

- No known-vulnerable dependencies (`npm audit` / equivalent), lockfile committed.
- Production errors don't leak stack traces, queries or internal paths to the browser.
- Debug routes, test accounts and admin panels are removed or protected.

## 8. Before going live

- Run through the app logged out, as a second user, and with tampered requests (changed IDs, missing fields, huge inputs).
- Confirm backups exist for anything with user data.
- Write the result as a short table: section, status, what was fixed, what is left for the user to decide.

---
Written in own words from public "vibe coding security checklist" material; no third-party text copied.
License: CC-BY-NC-SA-4.0 — © DerHeimer, https://github.com/DerHeimer/claude-auto-kit (see NOTICE.md)
