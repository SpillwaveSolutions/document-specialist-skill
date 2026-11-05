# API Documentation: The Stripe Gold Standard

---
TOKEN_BUDGET: 180
TIER: 3
LOAD_TRIGGER: On-demand when creating API documentation
DEPENDENCIES: None
---

## 5.1 The Gold Standard: Stripe API

Stripe's API documentation is widely considered the best. Key features:

### 1. Three-Column Layout

- **Left**: Navigation (organized by resource)
- **Middle**: Conceptual explanation, parameter descriptions
- **Right**: Interactive code examples in multiple languages

**Benefit**: Users can read and try code simultaneously

---

### 2. Core Concepts First

Teaches the model before teaching the methods.

**Example**: Before showing PaymentIntent endpoints, explains the PaymentIntent state machine and lifecycle.

**Benefit**: Users understand the "why" before the "how"

---

### 3. Interactive & Personalized

- Pre-filled with user's test API keys
- Click "Run" to execute API calls in sandbox
- See real responses

**Benefit**: Reduces time-to-first-API-call from hours to minutes

---

### 4. Clear Auth & Errors

- **Authentication**: Dedicated page explaining Bearer tokens, test vs. live keys
- **Errors**: Comprehensive error codes with explanations and solutions

**Benefit**: Reduces support burden for common issues

---

### 5. Code Examples in Multiple Languages

- cURL (for testing)
- Python, Ruby, Node.js, PHP, Java, Go (for implementation)
- Each example is complete and runnable

**Benefit**: Developers can copy-paste to get started quickly

---

### Lessons for Your API Docs

1. **Teach concepts first**: Don't just list endpoints
2. **Make it interactive**: Sandbox or code playground
3. **Show complete examples**: Not just request, but full response too
4. **Organize by user goal**: "Accept a payment" not "POST /charges"
5. **Invest in search**: Users should find answers in <30 seconds

---

**End of Stripe Gold Standard Guide**
