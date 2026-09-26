# Security Policy

## Responsible Disclosure
If you discover a security vulnerability within the **Developer Intelligence Platform**, please report it directly to **Fahad Iqbal**. Do not create public issues regarding exploitable security flaws.

## Defensive Architecture Principles

### 1. Untrusted Code Isolation
All user-supplied source files, documentation, package manifests, and comments are treated as **untrusted data**.
- Code is NEVER executed or evaluated on the server.
- The platform contains no dynamic `eval()`, `exec()`, or child process triggers for user code.
- Inputs are parsed purely for static AST and regex inspection.

### 2. Prompt Injection Defense
Repository files often contain natural language instructions. To prevent prompt injection attacks:
- Input files are wrapped in isolated context delimiters (`### BEGIN UNTRUSTED CONTEXT`).
- Delimiters within untrusted files are escaped.
- System prompt instructions explicitly forbid models from obeying commands embedded within user code context.

### 3. Path Traversal Neutralization (CWE-22)
- All incoming file paths are sanitized via `sanitizePath()`.
- Upward traversal segments (`..`) and absolute filesystem references are stripped.
- Dotfiles (such as `.env`, `.git/config`, `.DS_Store`) and sensitive directories (such as `node_modules/`, `.git/`) are ignored by default.

### 4. Authentication & Password Hardening
- Passwords are never stored in plaintext. Passwords are salted and hashed using `bcryptjs` (work factor 10).
- Session tokens are stateless JSON Web Tokens (JWT) signed with a minimum 32-character secret key.
- Cookies are configured with `HttpOnly`, `SameSite=Lax`, and `Secure` attributes in production.
