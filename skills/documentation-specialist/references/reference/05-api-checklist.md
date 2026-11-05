# API Documentation: Checklist

---
TOKEN_BUDGET: 200
TIER: 3
LOAD_TRIGGER: On-demand when auditing API documentation
DEPENDENCIES: 05-api-openapi.md
---

## 5.3 API Documentation Checklist

### Essential Elements

- [ ] **Base URL and versioning** (e.g., `https://api.example.com/v1`, `/v2`)
- [ ] **Authentication method** (JWT, OAuth2, API key)
  - [ ] How to obtain credentials
  - [ ] How to include in requests (header, query param)
  - [ ] Token expiration and refresh
- [ ] **All endpoints with HTTP methods** (GET, POST, PUT, DELETE, PATCH)
- [ ] **Request parameters** (query, path, body)
  - [ ] Required vs. optional
  - [ ] Data types and formats
  - [ ] Validation rules
- [ ] **Request/response schemas** with examples
- [ ] **Status codes** (200, 201, 400, 401, 404, 500)
  - [ ] What each code means
  - [ ] Example responses for each code
- [ ] **Error responses with codes and messages**
  - [ ] Error format structure
  - [ ] Common error codes
  - [ ] How to resolve errors
- [ ] **Rate limiting policies**
  - [ ] Limits per endpoint
  - [ ] Time windows
  - [ ] Headers to check remaining quota
- [ ] **Code examples in multiple languages**
  - [ ] cURL (minimum)
  - [ ] Python, JavaScript, Java (recommended)
  - [ ] Complete, runnable examples
- [ ] **Getting Started tutorial**
  - [ ] Register for API key
  - [ ] Make first API call
  - [ ] Common workflows
- [ ] **Webhooks documentation** (if applicable)
  - [ ] Available events
  - [ ] Payload schemas
  - [ ] Signature verification

### Quality Indicators

**Good API docs have:**
- ✅ Interactive sandbox or playground
- ✅ Searchable reference
- ✅ Conceptual guides (not just reference)
- ✅ Change log (versioned, dated)
- ✅ SDKs or client libraries

**Great API docs have:**
- ✅ Personalized with user's API key
- ✅ Code generators (Postman collections, SDKs)
- ✅ Real-world use case tutorials
- ✅ Performance and optimization tips
- ✅ Community forum or support channel

---

**End of API Documentation Checklist**
