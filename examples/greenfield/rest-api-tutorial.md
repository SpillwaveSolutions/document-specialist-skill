# Tutorial: Build a Task API with Node.js and Express

**Learning Objective**: Create a fully functional REST API with CRUD operations, authentication, and database persistence in under 45 minutes.

**Level**: Intermediate
**Time**: ~45 minutes
**Last Updated**: January 18, 2025

---

## What You'll Build

By the end of this tutorial, you'll have created:
- A REST API with full CRUD operations for tasks
- JWT-based authentication (register, login)
- SQLite database for data persistence
- Error handling and validation
- Automated tests with Jest

**Technologies Used**:
- Node.js 18+
- Express.js 4.x
- SQLite3 (via better-sqlite3)
- JWT for authentication
- Jest for testing

**Complete Code**: https://github.com/example/task-api-tutorial

---

## Prerequisites

### Required Knowledge
- JavaScript ES6+ syntax (arrow functions, destructuring, async/await)
- Basic understanding of REST APIs (GET, POST, PUT, DELETE)
- Familiarity with command-line tools

### Required Tools
- [ ] Node.js 18 or higher (`node --version`)
- [ ] npm 8+ or yarn (`npm --version`)
- [ ] Text editor (VS Code recommended)
- [ ] Git (for cloning starter)

### Optional (Recommended)
- [ ] Postman or Insomnia (for API testing)
- [ ] REST Client VS Code extension

**Verify your setup**:
```bash
node --version  # v18.0.0 or higher
npm --version   # 8.0.0 or higher
```

---

## Project Setup (5 Minutes)

### Initialize Project
```bash
mkdir task-api
cd task-api
npm init -y
```

### Install Dependencies
```bash
npm install express better-sqlite3 jsonwebtoken bcrypt dotenv
npm install --save-dev jest supertest nodemon
```

### Project Structure
Create these files:
```bash
touch server.js db.js routes/auth.js routes/tasks.js middleware/auth.js .env
```

**Final structure**:
```
task-api/
├── server.js           # Express app entry point
├── db.js               # Database setup
├── routes/
│   ├── auth.js         # Authentication endpoints
│   └── tasks.js        # Task CRUD endpoints
├── middleware/
│   └── auth.js         # JWT verification middleware
├── tests/
│   └── api.test.js     # Integration tests
├── .env                # Environment variables
└── package.json
```

### Configure Environment
Create `.env`:
```env
PORT=3000
JWT_SECRET=your-secret-key-change-in-production
NODE_ENV=development
```

### Add Scripts to package.json
```json
{
  "scripts": {
    "start": "node server.js",
    "dev": "nodemon server.js",
    "test": "jest --coverage"
  }
}
```

### Verify Setup
Create minimal `server.js`:
```javascript
const express = require('express');
const app = express();

app.get('/', (req, res) => {
  res.json({ message: 'Task API is running' });
});

const PORT = process.env.PORT || 3000;
app.listen(PORT, () => {
  console.log(`Server running on port ${PORT}`);
});
```

Start server:
```bash
npm run dev
```

Visit `http://localhost:3000` → should see: `{"message":"Task API is running"}`

✅ **Checkpoint**: If you see the message, your environment is ready!

---

## Step 1: Set Up Database

### What We're Building
A SQLite database with two tables: `users` (authentication) and `tasks` (CRUD operations). We're using SQLite for simplicity, but the patterns apply to PostgreSQL, MySQL, etc.

### The Code
Create `db.js`:
```javascript
const Database = require('better-sqlite3');
const path = require('path');

// Initialize database
const db = new Database(path.join(__dirname, 'tasks.db'));

// Create tables
db.exec(`
  CREATE TABLE IF NOT EXISTS users (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    username TEXT UNIQUE NOT NULL,
    password TEXT NOT NULL,
    created_at DATETIME DEFAULT CURRENT_TIMESTAMP
  )
`);

db.exec(`
  CREATE TABLE IF NOT EXISTS tasks (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    title TEXT NOT NULL,
    description TEXT,
    completed BOOLEAN DEFAULT 0,
    user_id INTEGER NOT NULL,
    created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES users(id)
  )
`);

console.log('✅ Database initialized');

module.exports = db;
```

### Explanation
**Key Concepts**:
- **better-sqlite3**: Synchronous SQLite library (faster than async for simple operations)
- **Line 8-15**: Users table with unique username constraint
- **Line 17-26**: Tasks table with foreign key to users
- **AUTOINCREMENT**: SQLite auto-generates IDs

💡 **Why SQLite?**: Perfect for development/learning. In production, use PostgreSQL/MySQL with connection pooling.

### Test It
Add to `server.js` (top):
```javascript
require('dotenv').config();
const db = require('./db');  // Initialize database
```

Restart server:
```bash
npm run dev
```

**Expected Output**:
```
✅ Database initialized
Server running on port 3000
```

You should see a `tasks.db` file created in your project directory.

---

## Step 2: Implement Authentication

### What We're Building
User registration and login with JWT tokens. Passwords are hashed with bcrypt (never stored plain-text!).

### The Code
Create `routes/auth.js`:
```javascript
const express = require('express');
const router = express.Router();
const bcrypt = require('bcrypt');
const jwt = require('jsonwebtoken');
const db = require('../db');

// Register new user
router.post('/register', async (req, res) => {
  try {
    const { username, password } = req.body;

    // Validate input
    if (!username || !password) {
      return res.status(400).json({ error: 'Username and password required' });
    }

    if (password.length < 6) {
      return res.status(400).json({ error: 'Password must be at least 6 characters' });
    }

    // Hash password
    const hashedPassword = await bcrypt.hash(password, 10);

    // Insert user
    const stmt = db.prepare('INSERT INTO users (username, password) VALUES (?, ?)');
    const result = stmt.run(username, hashedPassword);

    res.status(201).json({
      message: 'User created successfully',
      userId: result.lastInsertRowid
    });
  } catch (error) {
    if (error.code === 'SQLITE_CONSTRAINT') {
      return res.status(409).json({ error: 'Username already exists' });
    }
    res.status(500).json({ error: 'Registration failed' });
  }
});

// Login user
router.post('/login', async (req, res) => {
  try {
    const { username, password } = req.body;

    // Find user
    const user = db.prepare('SELECT * FROM users WHERE username = ?').get(username);

    if (!user) {
      return res.status(401).json({ error: 'Invalid credentials' });
    }

    // Verify password
    const validPassword = await bcrypt.compare(password, user.password);

    if (!validPassword) {
      return res.status(401).json({ error: 'Invalid credentials' });
    }

    // Generate JWT
    const token = jwt.sign(
      { userId: user.id, username: user.username },
      process.env.JWT_SECRET,
      { expiresIn: '24h' }
    );

    res.json({
      message: 'Login successful',
      token,
      user: { id: user.id, username: user.username }
    });
  } catch (error) {
    res.status(500).json({ error: 'Login failed' });
  }
});

module.exports = router;
```

### Explanation
**Security Concepts**:
- **bcrypt.hash(password, 10)**: Hashes password with 10 salt rounds (industry standard)
- **bcrypt.compare()**: Safely compares plain-text password with hash
- **JWT**: Stateless authentication token (no session storage needed)
- **expiresIn**: Token auto-expires after 24 hours

**Error Handling**:
- **SQLITE_CONSTRAINT**: Catches duplicate username error
- **401 Unauthorized**: Invalid credentials (vague for security - don't reveal if username or password is wrong)

### Wire It Up
Update `server.js`:
```javascript
require('dotenv').config();
const express = require('express');
const db = require('./db');
const authRoutes = require('./routes/auth');

const app = express();

// Middleware
app.use(express.json());

// Routes
app.use('/auth', authRoutes);

app.get('/', (req, res) => {
  res.json({ message: 'Task API is running' });
});

const PORT = process.env.PORT || 3000;
app.listen(PORT, () => {
  console.log(`Server running on port ${PORT}`);
});
```

### Test It
**Register a user**:
```bash
curl -X POST http://localhost:3000/auth/register \
  -H "Content-Type: application/json" \
  -d '{"username":"alice","password":"secret123"}'
```

**Expected Response**:
```json
{
  "message": "User created successfully",
  "userId": 1
}
```

**Login**:
```bash
curl -X POST http://localhost:3000/auth/login \
  -H "Content-Type: application/json" \
  -d '{"username":"alice","password":"secret123"}'
```

**Expected Response**:
```json
{
  "message": "Login successful",
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "user": {"id": 1, "username": "alice"}
}
```

🔒 **Save this token** - you'll need it for task operations!

### Checkpoint ✅
You should now have:
- Working user registration
- Secure password hashing
- JWT token generation
- Error handling for duplicate users

---

## Step 3: Protect Routes with Middleware

### What We're Building
Middleware that verifies JWT tokens before allowing access to protected routes.

### The Code
Create `middleware/auth.js`:
```javascript
const jwt = require('jsonwebtoken');

function authenticateToken(req, res, next) {
  // Get token from header
  const authHeader = req.headers['authorization'];
  const token = authHeader && authHeader.split(' ')[1]; // "Bearer <token>"

  if (!token) {
    return res.status(401).json({ error: 'Access token required' });
  }

  // Verify token
  jwt.verify(token, process.env.JWT_SECRET, (err, user) => {
    if (err) {
      return res.status(403).json({ error: 'Invalid or expired token' });
    }

    // Attach user to request object
    req.user = user;
    next(); // Proceed to route handler
  });
}

module.exports = authenticateToken;
```

### Explanation
**Middleware Pattern**:
- **Line 6**: Extract token from `Authorization: Bearer <token>` header
- **Line 13**: Verify token using same secret used to sign it
- **Line 18**: Attach decoded user info to `req.user` for route handlers
- **Line 19**: Call `next()` to proceed to route handler

**Error Handling**:
- **401 Unauthorized**: No token provided
- **403 Forbidden**: Token invalid or expired

---

## Step 4: Implement Task CRUD Operations

### The Code
Create `routes/tasks.js`:
```javascript
const express = require('express');
const router = express.Router();
const db = require('../db');
const authenticateToken = require('../middleware/auth');

// All routes require authentication
router.use(authenticateToken);

// Get all tasks for current user
router.get('/', (req, res) => {
  const tasks = db.prepare('SELECT * FROM tasks WHERE user_id = ? ORDER BY created_at DESC')
    .all(req.user.userId);
  res.json(tasks);
});

// Create new task
router.post('/', (req, res) => {
  const { title, description } = req.body;

  if (!title) {
    return res.status(400).json({ error: 'Title required' });
  }

  const stmt = db.prepare('INSERT INTO tasks (title, description, user_id) VALUES (?, ?, ?)');
  const result = stmt.run(title, description || '', req.user.userId);

  res.status(201).json({
    id: result.lastInsertRowid,
    title,
    description,
    completed: false,
    user_id: req.user.userId
  });
});

// Update task
router.put('/:id', (req, res) => {
  const { title, description, completed } = req.body;

  const stmt = db.prepare(`
    UPDATE tasks
    SET title = ?, description = ?, completed = ?
    WHERE id = ? AND user_id = ?
  `);

  const result = stmt.run(title, description, completed ? 1 : 0, req.params.id, req.user.userId);

  if (result.changes === 0) {
    return res.status(404).json({ error: 'Task not found' });
  }

  res.json({ message: 'Task updated successfully' });
});

// Delete task
router.delete('/:id', (req, res) => {
  const stmt = db.prepare('DELETE FROM tasks WHERE id = ? AND user_id = ?');
  const result = stmt.run(req.params.id, req.user.userId);

  if (result.changes === 0) {
    return res.status(404).json({ error: 'Task not found' });
  }

  res.json({ message: 'Task deleted successfully' });
});

module.exports = router;
```

### Wire It Up
Add to `server.js`:
```javascript
const taskRoutes = require('./routes/tasks');
app.use('/tasks', taskRoutes);  // Add after auth routes
```

### Test Full Workflow
**1. Register & Login** (get token):
```bash
TOKEN=$(curl -s -X POST http://localhost:3000/auth/login \
  -H "Content-Type: application/json" \
  -d '{"username":"alice","password":"secret123"}' \
  | grep -o '"token":"[^"]*' | cut -d'"' -f4)
```

**2. Create Task**:
```bash
curl -X POST http://localhost:3000/tasks \
  -H "Authorization: Bearer $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"title":"Build Task API","description":"Complete tutorial"}'
```

**3. Get All Tasks**:
```bash
curl http://localhost:3000/tasks \
  -H "Authorization: Bearer $TOKEN"
```

**4. Update Task**:
```bash
curl -X PUT http://localhost:3000/tasks/1 \
  -H "Authorization: Bearer $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"title":"Build Task API","description":"Tutorial completed!","completed":true}'
```

**5. Delete Task**:
```bash
curl -X DELETE http://localhost:3000/tasks/1 \
  -H "Authorization: Bearer $TOKEN"
```

---

## What You've Learned

✅ RESTful API design (CRUD operations)
✅ JWT authentication (register, login, protected routes)
✅ Secure password handling with bcrypt
✅ SQLite database with foreign keys
✅ Express middleware pattern
✅ Error handling and validation
✅ HTTP status codes (200, 201, 400, 401, 403, 404, 500)

---

## Challenge Yourself

1. **Easy**: Add pagination to GET /tasks (limit, offset)
2. **Medium**: Add task filtering by completed status
3. **Hard**: Implement refresh tokens for extended sessions

---

## Next Steps

- [Add Testing with Jest](link)
- [Deploy to Production](link)
- [Add PostgreSQL](link)
- [API Documentation with Swagger](link)

---

**Complete Code**: https://github.com/example/task-api-tutorial
**Tutorial Author**: Documentation Specialist Skill
**Last Tested**: January 18, 2025 with Node 18.17.0
