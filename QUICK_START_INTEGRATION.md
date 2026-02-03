# 🚀 QUICK START - Frontend & Backend Integration

## 30-Second Setup

### Terminal 1: Start Backend
```bash
cd backend
npm start
```

Wait for: `[SERVER] Running on http://localhost:3000`

### Terminal 2: Start Frontend
```bash
npm run dev
```

Wait for: `Local: http://localhost:5173`

### Browser
Open: `http://localhost:5173`

---

## 📝 Login Credentials

**Admin Account:**
- Email: `admin@library.com`
- Password: `admin123`

**Student Accounts:**
- alice@university.edu / student123
- bob@university.edu / student123
- charlie@university.edu / student123

---

## ✨ What Works

### ✅ User Management
- View all users
- Search users
- Create new users
- Blacklist/unblacklist users
- User statistics

### ✅ Book Management
- Browse all books
- Search books by title/author
- Add new books
- Update book details
- Delete books
- Track availability

### ✅ Issue & Return
- Issue books to students
- Track due dates
- Return books
- Condition tracking

### ✅ Fine System
- Automatic fine calculation
- ₹10 per day after 5-day grace period
- ₹100 maximum cap
- Auto-blacklist at ₹100
- Fine payment tracking

### ✅ Activity Logging
- Track all user actions
- View activity history
- Activity summary reports

---

## 📚 Database

### Collections
1. **Users** - Admin & Students with profiles
2. **Books** - Library inventory
3. **IssuedBooks** - Book issue/return tracking
4. **Fines** - Fine calculations & payments
5. **ActivityLogs** - Complete audit trail

### Sample Data
- 1 Admin user
- 3 Student users
- 6 Sample books

---

## 🔧 Backend Endpoints

**All 25+ endpoints are accessible:**

```
Users:     GET/POST/PUT /api/users, /api/users/:id
Books:     GET/POST/PUT/DELETE /api/books, /api/books/:id
Issues:    POST /api/issues/issue-book, /issues/:id/return
Fines:     GET /api/fines/user/:userId, POST /api/fines/:id/pay
Activities: GET /api/activities, /api/activities/summary
```

---

## 🎯 File Structure

```
Project/
├── backend/
│   ├── app.js (Express server)
│   ├── database/ (MongoDB operations)
│   ├── fineAndDiscipline.js (Fine logic)
│   ├── package.json
│   └── .env (MongoDB connection)
├── src/
│   ├── config/apiClient.ts ⭐ NEW - API client
│   ├── pages/
│   │   ├── Login.tsx ⭐ UPDATED - Real auth
│   │   ├── Dashboard.tsx ⭐ UPDATED - Real data
│   │   ├── Books.tsx ⭐ UPDATED - Backend API
│   │   ├── Users.tsx ⭐ UPDATED - Backend API
│   │   └── ...
│   └── ...
└── INTEGRATION_GUIDE.md ⭐ NEW - Detailed guide
```

---

## 🐛 If Something Doesn't Work

### Backend won't start?
```bash
# Check if MongoDB is running
Get-Service MongoDB

# Kill process on port 3000
Stop-Process -Name node
```

### Frontend can't connect?
- Check backend is running on http://localhost:3000
- Frontend will fallback to demo mode automatically

### Database issues?
- Check MongoDB is running locally
- Verify connection string in backend/.env
- Run `node initializeDB.js` to reinitialize data

---

## 📖 Full Documentation

See **INTEGRATION_GUIDE.md** for:
- Detailed setup instructions
- All API endpoints
- Database schema
- Fine calculation rules
- Troubleshooting guide
- Development guide

---

## 🎉 You're Ready!

Just run:
```bash
cd backend && npm start   # Terminal 1
npm run dev              # Terminal 2
# Open http://localhost:5173 in browser
# Login with admin@library.com / admin123
```

**Everything is connected and working!**
