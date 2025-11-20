# Tutorial: [Build/Create/Implement Specific Project]

**Learning Objective**: [Clear statement of what developers will learn - be specific!]

**Level**: [Beginner/Intermediate/Advanced]
**Time**: ~[X] minutes
**Last Updated**: [Date]

---

## What You'll Build

By the end of this tutorial, you'll have created:
- [Deliverable 1 - be concrete, e.g., "A REST API with authentication"]
- [Deliverable 2 - e.g., "User registration and login endpoints"]
- [Deliverable 3 - e.g., "Database persistence with SQLite"]

**Technologies Used**:
- [Language/Framework 1, e.g., "Node.js 18+"]
- [Language/Framework 2, e.g., "Express.js 4.x"]
- [Tool/Library 3, e.g., "JWT for authentication"]

**Complete Code**: [Link to GitHub repository]

---

## Prerequisites

### Required Knowledge
- [Skill 1, e.g., "JavaScript ES6+ syntax (arrow functions, async/await)"]
- [Skill 2, e.g., "Basic understanding of REST APIs"]
- [Skill 3, e.g., "Familiarity with command-line tools"]

### Required Tools
- [ ] [Tool 1 with version, e.g., "Node.js 18 or higher"]
- [ ] [Tool 2, e.g., "npm or yarn package manager"]
- [ ] [Tool 3, e.g., "Text editor (VS Code recommended)"]
- [ ] [Tool 4, e.g., "Git (for cloning starter code)"]

### Optional (Recommended)
- [ ] [Optional tool, e.g., "Postman or curl for API testing"]
- [ ] [Optional knowledge, e.g., "Docker (for containerization section)"]

**Verify your setup**:
```bash
node --version  # Should be v18.0.0 or higher
npm --version   # Should be 8.0.0 or higher
```

---

## Project Setup (5 Minutes)

### Option 1: Clone Starter Project
```bash
git clone https://github.com/example/tutorial-starter
cd tutorial-starter
npm install
```

### Option 2: Start from Scratch
```bash
mkdir my-project
cd my-project
npm init -y
npm install express dotenv
```

### Verify Setup
Start the development server:
```bash
npm run dev
```

Visit `http://localhost:3000` - you should see:
```
Hello World
```

✅ **Checkpoint**: If you see "Hello World", your environment is ready!

---

## Step 1: [First Major Concept/Feature]

### What We're Building
[Brief explanation of what this step accomplishes and WHY it's important]

### The Code
Create `[filename]`:
```javascript
// [Brief description of file purpose]
const express = require('express');
const app = express();

// Middleware
app.use(express.json());

// Routes
app.get('/', (req, res) => {
  res.json({ message: 'Welcome to the API' });
});

// Start server
const PORT = process.env.PORT || 3000;
app.listen(PORT, () => {
  console.log(`Server running on port ${PORT}`);
});

module.exports = app;  // For testing
```

### Explanation
**Key Concepts**:
- **Line 1-2**: [Explain imports and why we need them]
- **Line 5**: [Explain middleware and its purpose]
- **Line 8-10**: [Explain route handler]

💡 **Why This Matters**: [Explain the concept's real-world relevance]

### Test It
Run the server:
```bash
node server.js
```

Test the endpoint:
```bash
curl http://localhost:3000
```

**Expected Output**:
```json
{"message":"Welcome to the API"}
```

### Common Errors
❌ **Error: "EADDRINUSE"**
- **Cause**: Port 3000 already in use
- **Fix**: Kill process on port 3000 or change PORT in code

---

## Step 2: [Second Major Concept/Feature]

### What We're Building
[Explanation - build on previous step]

### The Code
Update `[filename]` to add [feature]:
```javascript
// Add new imports
const bcrypt = require('bcrypt');
const jwt = require('jsonwebtoken');

// New route for user registration
app.post('/register', async (req, res) => {
  try {
    const { username, password } = req.body;

    // Validate input
    if (!username || !password) {
      return res.status(400).json({ error: 'Username and password required' });
    }

    // Hash password
    const hashedPassword = await bcrypt.hash(password, 10);

    // Save user (simplified - no database yet)
    users.push({ username, password: hashedPassword });

    res.status(201).json({ message: 'User created successfully' });
  } catch (error) {
    res.status(500).json({ error: 'Registration failed' });
  }
});
```

### Explanation
**New Concepts**:
- **bcrypt**: [Explain password hashing and security]
- **Async/Await**: [Explain asynchronous operations]
- **Error Handling**: [Explain try/catch pattern]

**Security Note**: 🔒 Never store plain-text passwords!

### Test It
Create a new user:
```bash
curl -X POST http://localhost:3000/register \
  -H "Content-Type: application/json" \
  -d '{"username":"alice","password":"secret123"}'
```

**Expected Output**:
```json
{"message":"User created successfully"}
```

### Checkpoint ✅
You should now have:
- Working Express server
- User registration endpoint
- Password hashing with bcrypt

---

## Step 3: [Third Major Concept/Feature]

[Follow same pattern: What we're building → Code → Explanation → Test → Common Errors]

---

## Step 4: [Additional Steps as Needed]

[Continue progressive learning pattern]

---

## Testing Your Application

### Unit Tests
Create `tests/api.test.js`:
```javascript
const request = require('supertest');
const app = require('../server');

describe('User Registration', () => {
  it('should create a new user', async () => {
    const res = await request(app)
      .post('/register')
      .send({ username: 'bob', password: 'test123' });

    expect(res.statusCode).toBe(201);
    expect(res.body.message).toBe('User created successfully');
  });
});
```

Run tests:
```bash
npm test
```

---

## Extensions & Next Steps

### What You've Learned
✅ [Skill/concept 1 learned]
✅ [Skill/concept 2 learned]
✅ [Skill/concept 3 learned]

### Challenge Yourself
Try adding these features on your own:
1. **Easy**: [Beginner challenge, e.g., "Add email validation"]
2. **Medium**: [Intermediate challenge, e.g., "Add password reset functionality"]
3. **Hard**: [Advanced challenge, e.g., "Add OAuth2 authentication"]

### Next Tutorials
- [Related tutorial 1]
- [Related tutorial 2]
- [Advanced tutorial building on this]

### Further Reading
- [Link to deeper documentation]
- [Link to related concepts]
- [Link to production deployment guide]

---

## Complete Code

The complete working code for this tutorial is available at:
**GitHub**: [Repository URL]

**Project Structure**:
```
project/
├── server.js
├── routes/
│   ├── auth.js
│   └── users.js
├── middleware/
│   └── authenticate.js
├── tests/
│   └── api.test.js
├── package.json
└── .env.example
```

---

## Troubleshooting

### Common Issues

**Module not found errors**
- Run `npm install` to install all dependencies
- Check package.json includes all required packages

**Port already in use**
- Change PORT in .env file
- Kill process: `lsof -ti:3000 | xargs kill`

**Authentication not working**
- Verify JWT_SECRET in .env
- Check token expiration time
- Ensure Authorization header format: `Bearer <token>`

---

## Additional Resources

**Documentation**:
- [Official docs link]
- [API reference link]

**Tools**:
- [Postman Collection](link)
- [Insomnia Workspace](link)

**Community**:
- [Forum/Discord link]
- [Stack Overflow tag]

---

**Tutorial Author**: [Name]
**Last Tested**: [Date] with [version info]
**Feedback**: [How to provide feedback on tutorial]
