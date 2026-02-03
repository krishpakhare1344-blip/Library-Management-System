# Frontend & Backend Integration - Complete Setup Guide

## ✅ Current Status

### Backend Server (Node.js + Express)
- **Status**: Running on `http://localhost:3000`
- **Database**: MongoDB (Local instance)
- **Files Created**: 11 core backend modules + comprehensive API
- **Sample Data**: Initialized (admin@library.com / admin123)

### Frontend Application (React + Vite)
- **Status**: Running on `http://localhost:5173`
- **Framework**: React 18, TypeScript, Tailwind CSS
- **API Client**: Configured in `src/config/apiClient.ts`

---

## 🚀 How to Use

### Step 1: Start the Backend Server

```bash
cd backend
npm install          # Only needed first time
npm start            # Starts server on port 3000
```

Or run directly:
```bash
node app.js
```

**Expected Output:**
```
[DB] Connected to MongoDB successfully
[SERVER] Running on http://localhost:3000
[SERVER] API Documentation available at http://localhost:3000
```

### Step 2: Start the Frontend (if not already running)

```bash
# In a new terminal, from project root
npm run dev
```

Frontend will be available at `http://localhost:5173`

### Step 3: Access the Application

1. **Open Browser**: http://localhost:5173
2. **Login with Sample Credentials**:
   - Email: `admin@library.com`
   - Password: `admin123`

Or create a new account as needed.

---

## 📚 Sample Data Available

### Admin User
- **Email**: admin@library.com
- **Password**: admin123
- **Role**: admin

### Sample Students
- **alice@university.edu** / student123
- **bob@university.edu** / student123
- **charlie@university.edu** / student123

### Sample Books (6 books loaded)
1. The Great Gatsby
2. To Kill a Mockingbird
3. 1984
4. Introduction to Algorithms
5. The Selfish Gene
6. Python for Data Analysis

---

## 🔌 API Endpoints (25+ Available)

### User Endpoints
- `GET /api/users` - List all users
- `GET /api/users/:userId` - Get specific user
- `POST /api/users` - Create new user
- `PUT /api/users/:userId` - Update user
- `POST /api/users/:userId/blacklist` - Blacklist user
- `POST /api/users/:userId/unblacklist` - Unblacklist user
- `GET /api/users/:userId/stats` - Get user statistics

### Book Endpoints
- `GET /api/books` - List all books
- `GET /api/books/:bookId` - Get specific book
- `POST /api/books` - Add new book
- `PUT /api/books/:bookId` - Update book
- `DELETE /api/books/:bookId` - Delete book
- `GET /api/books/available` - Get available books

### Issue/Return Endpoints
- `POST /api/issues/issue-book` - Issue book to user
- `POST /api/issues/:issuedBookId/return` - Return book
- `GET /api/issues/user/:userId` - Get user's issued books
- `GET /api/issues/overdue` - Get overdue books

### Fine Endpoints
- `GET /api/fines/user/:userId` - Get user's pending fines
- `POST /api/fines/:fineId/pay` - Pay a fine
- `GET /api/fines/unpaid` - Get all unpaid fines

### Activity Log Endpoints
- `GET /api/activities` - Get activity logs
- `GET /api/activities/summary` - Get activity summary

---

## 🎯 Frontend Integration

### API Client Configuration

The frontend uses a centralized API client configured in `src/config/apiClient.ts`

**All functions are exported and can be imported as:**

```typescript
import {
  getAllUsers,
  getAllBooks,
  issueBook,
  returnBook,
  getUserPendingFines,
  payFine,
  getActivityLogs,
  // ... and 20+ more functions
} from '../config/apiClient'
```

### Updated Pages with Backend Integration

1. **Login Page** (`src/pages/Login.tsx`)
   - Authenticates users against the backend
   - Falls back to demo mode if backend unavailable
   - Stores user data in localStorage

2. **Dashboard** (`src/pages/Dashboard.tsx`)
   - Fetches real data from backend
   - Shows books, users, overdue items, fines
   - Manages book issues and returns

3. **Books Page** (`src/pages/Books.tsx`)
   - Lists books from backend database
   - Search and filter functionality
   - Add/edit/delete books

4. **Users Page** (`src/pages/Users.tsx`)
   - Lists all users from backend
   - Blacklist/unblacklist users
   - User management

---

## 🔄 Database Connection

### Current Setup
- **MongoDB**: Local instance on `mongodb://localhost:27017`
- **Database Name**: `library-management-system`
- **Connection**: Established on server startup

### Change Connection (if needed)

Edit `backend/.env`:
```env
# Local MongoDB
MONGO_URI=mongodb://localhost:27017/library-management-system

# Or MongoDB Atlas (cloud)
MONGO_URI=mongodb+srv://username:password@cluster.mongodb.net/library-management-system
```

---

## 🐛 Troubleshooting

### Issue: Backend won't start

**Solution 1**: Ensure MongoDB is running
```bash
# Windows
Get-Service MongoDB

# If not running
Start-Service MongoDB
```

**Solution 2**: Check if port 3000 is in use
```bash
Get-NetTCPConnection -LocalPort 3000
```

Kill the process:
```bash
Stop-Process -Id <PID> -Force
```

### Issue: Frontend can't connect to backend

**Solution**: Verify backend is running
```bash
# Check if server is responding
Invoke-WebRequest http://localhost:3000/api/users
```

If connection fails, the frontend automatically falls back to demo mode.

### Issue: MongoDB Connection Error

**Solution**: 
1. Ensure MongoDB is installed and running
2. Check MongoDB connection string in `.env`
3. Verify MongoDB service is started

---

## 📝 Fine Calculation Rules (Implemented)

- **Days 1-5 overdue**: Send reminder, NO fine
- **Day 6 onwards**: Fine = ₹10 per day
- **Maximum fine**: ₹100 cap
- **At ₹100 cap**: User automatically blacklisted
- **Blacklist effect**: Cannot issue new books

---

## 🔒 Automatic Features

### Cron Jobs (Scheduled Tasks)
- Daily fine check at 2:00 AM
- Automatic activity logging
- Database cleanup

### Activity Logging
Every action is logged:
- Book issues/returns
- Fine payments
- User blacklisting
- Profile updates
- Login/logout

### File Uploads
- Profile images (5MB max)
- Book covers (10MB max)
- Stored in `backend/uploads/`

---

## 📊 System Architecture

```
Frontend (React)
    ↓ (HTTP requests)
API Client (src/config/apiClient.ts)
    ↓ (REST API)
Backend (Express.js on port 3000)
    ↓ (Database operations)
MongoDB (Local instance)
```

---

## 🛠️ Development

### To modify API endpoints

Edit: `backend/app.js`

Example:
```javascript
app.get('/api/custom-endpoint', async (req, res) => {
  try {
    // Your logic here
    res.json({ success: true, data: [] })
  } catch (error) {
    res.status(400).json({ error: error.message })
  }
})
```

### To add new operations

Create file: `backend/database/newOperations.js`

Export functions and import in `app.js`:
```typescript
import * as newOps from './database/newOperations.js'
```

### To modify frontend pages

Edit any page in `src/pages/`

Import API functions:
```typescript
import { getAllBooks, getBookById } from '../config/apiClient'
```

---

## 📋 What's Included

### Backend Files (11 core modules)
✅ app.js - Main Express server
✅ database/connection.js - MongoDB connection
✅ database/schemas.js - Mongoose models
✅ database/fileUpload.js - File upload handler
✅ database/userOperations.js - User CRUD
✅ database/bookOperations.js - Book CRUD
✅ database/issuedBooksOperations.js - Issue/Return logic
✅ database/activityLog.js - Activity logging
✅ fineAndDiscipline.js - Fine calculation
✅ cronJobs.js - Scheduled tasks
✅ initializeDB.js - Database initialization

### Frontend Files (Updated)
✅ src/config/apiClient.ts - API client
✅ src/pages/Login.tsx - Authentication
✅ src/pages/Dashboard.tsx - Main dashboard
✅ src/pages/Books.tsx - Book management
✅ src/pages/Users.tsx - User management
✅ All existing components working

### Database
✅ 5 collections (Users, Books, IssuedBooks, Fines, ActivityLogs)
✅ Proper indexes for performance
✅ Sample data initialized

---

## 🎉 You're All Set!

The complete system is now:
- ✅ Backend running on port 3000
- ✅ Frontend running on port 5173
- ✅ MongoDB database connected
- ✅ Sample data loaded
- ✅ API client configured
- ✅ All pages connected to backend

**Start using the application!**

```bash
1. Terminal 1: cd backend && node app.js
2. Terminal 2: npm run dev
3. Browser: http://localhost:5173
4. Login: admin@library.com / admin123
```

---

## 📞 Support

If you need to:
- Add new features
- Modify API endpoints
- Change database schema
- Add authentication
- Deploy to production

All code is well-documented and ready for customization!
