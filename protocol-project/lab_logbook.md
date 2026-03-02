# Lab Logbook: Open Authorization Protocol

## Version 1 (Week 2) — Bare Bones

**File:** `OpenAuth_Simple.AnB`

**What changed:** Initial protocol design. Simplified by giving A a public key to avoid IDP complexity in the first iteration.

**Idea:** A requests authorization from IDP using symmetric key; IDP issues signed token; A forwards to P; P presents to B; B returns Photos.

**Modeling:** Data at B = constant `Photos`. All parties know all public keys initially.

**Problems:** OFMC may report issues if Goals are too strong. A having a key contradicts the scenario (A has no key).

---

## Version 2 (Week 2) — Static Analysis

**What changed:** Performed Dolev-Yao static analysis with passive intruder.

**Findings:** Intruder observes all messages. Without `shk(A,IDP)` cannot forge A's request. Without `sk(IDP)` cannot forge token. Structure of messages is visible.

**Problems:** None for passive intruder.

---

## Version 3 (Week 3) — A Without Key

**File:** `OpenAuth_Full.AnB`

**What changed:** Removed A's public/private key. A authenticates only via `shk(A,IDP)` (password-derived).

**Idea:** Password is shared secret; used for MAC/authentication only, not as encryption key for sensitive long-term data.

**Modeling:** IDP no longer has `pk(A)` since A has no key.

**Lazy intruder (P role):** Intruder receives token from A, forwards to B. Role P is executable. This is expected—P is a service; security is that only A (via IDP) can create tokens.

---

## Version 4 (Week 3) — Attack Consideration

**What changed:** Considered attack where intruder plays A.

**Findings:** Intruder would need `shk(A,IDP)` to authenticate as A. If password is guessable, intruder could try to guess. Week 6 task addresses this.

---

## Version 5 (Week 4) — Formats and Type-Flaw Resistance

**File:** `OpenAuth_Formats.AnB`

**What changed:** Added format tags `f_req`, `f_token`, `f_photos` to prevent type-flaw attacks.

**Modeling:** Each message type has distinct format; no two different message types can unify.

**Type-flaw resistance:** Verified that non-variable messages with unifier have same type.

---

## Version 6 (Week 4) — GetPublicKey

**File:** `GetPublicKey.AnB`

**What changed:** Separate protocol for A to obtain `pk(X)` from IDP. A initially knows only `pk(IDP)`.

**Idea:** Simplifies main protocol; A runs GetPublicKey for B and P before OpenAuth.

---

## Version 7 (Week 5) — TLS Channels

**File:** `OpenAuth_TLS.AnB`

**What changed:** Documented TLS channel variant. Standard AnB does not support channels; AnBx does. Kept message-passing version with comments.

**Modeling:** A-IDP and P-B over TLS (server-authenticated). Pseudonymous channels do not ensure freshness; nonce retained.

---

## Version 8 (Week 6) — Guessable Password

**What changed:** Marked `shk(A,IDP)` as guessable in OFMC (if supported).

**Findings:** Protocol remains secure for authorization flow. Password compromise allows impersonation of A to IDP—inherent to password auth. No amplification (e.g., password not used to encrypt tokens).

---

## Discussions / Teacher Input

- Clarified that "password not as encryption key" means we use it for authentication (MAC) only.
- Lazy intruder for P: forwarding is correct behavior; P is not a secret role.
- Format tags: follow lecture examples for type-flaw resistance.
