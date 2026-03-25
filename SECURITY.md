# Security Policy

> Libertad VZLA handles sensitive data in a high-risk geopolitical context. This document defines our security posture, threat model, and vulnerability disclosure program.

---

## ⚠️ Threat Model

### Adversary Profile

This platform is designed to resist threats from:

| Threat Actor | Capability | Mitigation Strategy |
|---|---|---|
| **State-level actors** | Network surveillance, DNS manipulation, legal coercion | Edge deployment, HTTPS enforcement, data minimization, no server-hosted PII logs |
| **Targeted attackers** | Credential stuffing, phishing, social engineering | MFA enforcement, role-based access, session management |
| **Supply chain attacks** | Compromised dependencies, typosquatting | Dependabot, lockfile auditing, minimal dependency surface |
| **Data exfiltration** | Database breaches, API abuse | RLS, input validation, rate limiting, audit logging |

### Attack Surface

- **Public-facing:** Marketing pages, news feed (read-only, no auth required)
- **Protected:** CMS dashboard, editorial workflows, admin panels (auth + RLS required)
- **Infrastructure:** Vercel Edge Network, Supabase managed PostgreSQL

---

## 🔐 Data Classification

All data handled by this platform is classified into tiers:

### Tier 1 — Critical (Maximum Protection)

- Source identities and contact information
- Denunciation/tip content and metadata
- User authentication credentials
- API keys and secrets

**Controls:** Encrypted at rest, encrypted in transit, access restricted to minimum viable roles, never logged, never cached client-side.

### Tier 2 — Sensitive (High Protection)

- Registered user profiles (names, emails)
- Editorial drafts and unpublished content
- CMS activity logs and audit trails
- Session tokens and auth state

**Controls:** Encrypted in transit, RLS-enforced access, server-side only processing, automatic expiration.

### Tier 3 — Public (Standard Protection)

- Published articles and media
- Public-facing marketing content
- Aggregated, anonymized analytics

**Controls:** Integrity validation, CDN caching, no PII embedded.

---

## 🛡️ Security Architecture

### Authentication & Access Control

- **Supabase Auth** with secure session management
- **Row-Level Security (RLS)** enforced on every table — no exceptions
- **Role-based access control (RBAC):** `viewer`, `editor`, `admin`, `superadmin`
- **Server-side auth verification** on all protected routes and Server Actions
- **No client-side auth decisions** — all authorization logic is server-enforced

### Data Protection

- **Environment variables** for all secrets — zero hardcoded credentials
- **`.env` files excluded** from version control via `.gitignore`
- **HTTPS-only** across all endpoints (enforced by Vercel)
- **Input validation** on all API endpoints and Server Actions
- **Output sanitization** to prevent XSS and injection attacks
- **CORS restrictions** on all API routes

### Infrastructure Security

- **Vercel Edge Network** — DDoS protection, automatic TLS, geographic distribution
- **Supabase managed PostgreSQL** — encrypted at rest, automated backups, network isolation
- **No self-hosted servers** — reduces attack surface
- **Automated dependency auditing** via Dependabot (`.github/dependabot.yml`)

### Source Protection

- **Data minimization** — we collect only what is strictly necessary
- **No IP logging** on submission endpoints
- **Metadata stripping** on user-submitted content
- **Journalist-source confidentiality** is an architectural requirement, not a policy choice

---

## 🚨 Incident Response

### Response Protocol

| Phase | Action | SLA |
|---|---|---|
| **Detection** | Automated monitoring, anomaly detection, user reports | Continuous |
| **Triage** | Severity classification (Critical/High/Medium/Low) | < 1 hour |
| **Containment** | Isolate affected systems, revoke compromised credentials | < 4 hours |
| **Eradication** | Root cause analysis, patch deployment | < 24 hours |
| **Recovery** | Service restoration, data integrity verification | < 48 hours |
| **Post-mortem** | Documented analysis, prevention measures | < 7 days |

### Severity Classification

- **Critical:** Data breach, authentication bypass, production downtime
- **High:** Privilege escalation, sensitive data exposure, XSS on authenticated pages
- **Medium:** Information disclosure (non-PII), CSRF, open redirects
- **Low:** Best practice violations, minor information leaks

---

## 📢 Vulnerability Disclosure

### Reporting a Vulnerability

If you discover a security vulnerability:

1. **DO NOT** create a public GitHub Issue
2. **DO NOT** disclose the vulnerability publicly before it is patched
3. **Email:** [security@luissambrano.dev](mailto:security@luissambrano.dev)
4. **Alternative:** Open a [private security advisory](https://github.com/LuisSambrano/libertad/security/advisories/new)

### What to Include

- Steps to reproduce the vulnerability
- Impact assessment (what data/systems are affected)
- Suggested fix (if applicable)
- Your contact information for follow-up

### Response SLAs

| Action | Timeline |
|---|---|
| Acknowledgment | **48 hours** |
| Initial assessment | **72 hours** |
| Patch development | **7 days** (critical), **14 days** (high), **30 days** (medium/low) |
| Public disclosure | After patch is deployed and verified |

### Safe Harbor

We will not pursue legal action against security researchers who:

- Act in good faith
- Avoid data destruction or service disruption
- Do not access data beyond what is necessary to demonstrate the vulnerability
- Report findings promptly and confidentially

---

## ✅ Security Checklist (Development)

All code contributions must satisfy:

- [ ] No hardcoded secrets, API keys, or credentials
- [ ] No `console.log` statements with sensitive data
- [ ] RLS policies verified on any new/modified tables
- [ ] Input validation on all new endpoints
- [ ] Server-side auth checks on all protected routes
- [ ] No `any` types in auth/security-related code
- [ ] Dependencies audited (`npm audit`)
- [ ] No `.env` files in staging or commits

---

## 📋 Supported Versions

| Version | Supported |
|---------|-----------|
| Latest  | ✅        |
| < 1.0   | ❌        |

---

## 🔄 Security Review Cadence

| Review Type | Frequency |
|---|---|
| Dependency audit (`npm audit`) | Every commit (CI) |
| Dependabot alerts | Continuous |
| RLS policy review | Every schema migration |
| Full security assessment | Quarterly |
| Penetration testing | Pre-launch, then annually |

---

_Last updated: 2026-03-25_
_Maintainer: Luis Sambrano — [security@luissambrano.dev](mailto:security@luissambrano.dev)_
