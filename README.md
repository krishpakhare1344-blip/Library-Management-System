# Library Management System

A modern, hackathon-ready frontend for a complete Library Management System with Analytics. Built with React, Vite, Tailwind CSS, and Chart.js.

## ✨ Features

### 📊 Dashboard
- Real-time overview with key metrics (Total Books, Issued Books, Active Users, Overdue Books)
- Interactive charts:
  - Bar chart: Most issued books
  - Line chart: Monthly book issue trends
  - Pie chart: Book categories distribution

### 📚 Books Management
- View complete library collection
- Add new books with full details
- Edit existing book information
- Delete books from inventory
- Real-time availability tracking
- Search and filter by title, author, or category
- Pagination support

### 📤 Issue & Return Module
- Issue books to users with automated due dates
- Track active and overdue books
- Record book returns
- View complete history of all issued/returned books
- Fine calculation support

### 👥 Users Management (Admin Only)
- Add new users with different roles
- Edit user information
- Toggle user status (active/inactive)
- View user statistics (books issued/returned)
- Role-based access control (Admin, Librarian, Student)

### 📈 Advanced Analytics (Admin Only)
- Comprehensive analytics dashboard
- Date range filtering
- Export reports as PDF, Excel, or CSV
- Detailed category distribution analysis
- Top issued books tracking
- Trend analysis and insights

### 📋 Activity Logs (Admin Only)
- Complete timeline view of all system activities
- Track book issuances, returns, and user registrations
- Activity breakdown by type
- Timestamped records for audit purposes

### 🎨 UI/UX Features
- **Dark/Light Mode**: Toggle between themes with persistent storage
- **Responsive Design**: Fully responsive on mobile, tablet, and desktop
- **Modern Design**: Glassmorphism effects with soft shadows
- **Smooth Animations**: Transitions and hover effects throughout
- **Toast Notifications**: User feedback for all actions
- **Loading States**: Skeleton screens for better UX

## 🛠️ Tech Stack

- **Frontend Framework**: React 18 with TypeScript
- **Build Tool**: Vite
- **Styling**: Tailwind CSS
- **Charts**: Chart.js with react-chartjs-2 and Recharts
- **Routing**: React Router v6
- **Icons**: Lucide React
- **State Management**: React Hooks

## 📋 Prerequisites

- Node.js 16+ 
- npm or yarn

## 🚀 Installation

1. **Clone the repository** (or extract the project files)
   ```bash
   cd library-management-system
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Start the development server**
   ```bash
   npm run dev
   ```

4. **Build for production**
   ```bash
   npm run build
   ```

5. **Preview production build**
   ```bash
   npm run preview
   ```

## 🔑 Demo Credentials

The application comes with pre-configured demo accounts for testing different roles:

### Admin Account
- **Email**: `admin@library.com`
- **Password**: `admin123`
- **Access**: Full system access including Users, Analytics, and Activity Logs

### Librarian Account
- **Email**: `librarian@library.com`
- **Password**: `lib123`
- **Access**: Books and Issue/Return management

### Student Account
- **Email**: `student@university.edu`
- **Password**: `student123`
- **Access**: View books and issue/return history

## 📁 Project Structure

```
src/
├── components/              # Reusable UI components
│   ├── Button.tsx          # Button component with variants
│   ├── Card.tsx            # Card container component
│   ├── Form.tsx            # Input, Select, TextArea components
│   ├── Layout.tsx          # Main layout with sidebar & navbar
│   ├── Modal.tsx           # Modal dialog component
│   ├── Skeleton.tsx        # Loading skeleton components
│   └── Toast.tsx           # Toast notification component
├── data/
│   └── mockData.ts         # Mock data and API functions
├── pages/                  # Page components
│   ├── Login.tsx           # Authentication page
│   ├── Dashboard.tsx       # Main dashboard with charts
│   ├── Books.tsx           # Books management page
│   ├── IssueReturn.tsx     # Issue/Return management
│   ├── Users.tsx           # User management (Admin)
│   ├── Analytics.tsx       # Analytics dashboard (Admin)
│   └── ActivityLogs.tsx    # Activity logs (Admin)
├── App.tsx                 # Main App component with routing
├── main.tsx                # App entry point
└── index.css               # Global styles

Configuration Files:
├── tailwind.config.js      # Tailwind CSS configuration
├── postcss.config.js       # PostCSS configuration
├── tsconfig.json           # TypeScript configuration
├── vite.config.ts          # Vite configuration
└── package.json            # Dependencies and scripts
```

## 🎯 Key Features Implementation

### 1. Authentication & Role-Based Access
- Three demo roles with different permissions
- Protected routes based on user role
- Persistent user state using localStorage

### 2. Dark Mode
- System-wide dark mode toggle
- Persisted preference in localStorage
- Smooth transitions between themes

### 3. Mock API
- Simulated API calls with delays
- Realistic data fetching behavior
- Ready for backend integration

### 4. Data Management
- Mock data for books, users, and issues
- CRUD operations on all entities
- Real-time updates across components

### 5. Advanced Charts
- Bar charts for categorical data
- Line charts for trends
- Pie charts for distribution
- Area charts for cumulative data
- Fully responsive chart containers

## 🔄 Backend Integration Guide

To integrate with a real backend:

1. **Update mockData.ts**
   - Replace mock API functions with actual HTTP requests
   - Use fetch or axios for API calls
   - Maintain the same function signatures

2. **Example API Integration**
   ```typescript
   // Replace mock function
   getBooks: async (): Promise<Book[]> => {
     const response = await fetch('/api/books')
     return response.json()
   }
   ```

3. **Update Authentication**
   - Replace demo credentials with real login endpoint
   - Implement JWT token handling
   - Add secure token storage

## 🎨 Customization

### Colors & Theme
- Modify `tailwind.config.js` to change primary colors
- Dark mode colors are automatically generated

### Components
- All components are in `src/components/`
- Reusable and fully customizable
- Use as building blocks for new features

### Pages
- Add new routes in `App.tsx`
- Create new pages in `src/pages/`
- Follow existing patterns for consistency

## 📝 Available Scripts

- `npm run dev` - Start development server
- `npm run build` - Build for production
- `npm run preview` - Preview production build
- `npm run lint` - Run ESLint (if configured)

## 🚀 Deployment

### Build
```bash
npm run build
```

### Serve
The `dist` folder contains the production-ready files. Deploy to:
- Vercel
- Netlify
- GitHub Pages
- Any static hosting service

### Environment Variables
Create a `.env` file for API endpoints:
```
VITE_API_URL=https://api.example.com
```

## 🐛 Troubleshooting

### Port Already in Use
```bash
npm run dev -- --port 3000
```

### Clear Cache
```bash
rm -rf node_modules package-lock.json
npm install
```

### Build Issues
```bash
npm run build -- --debug
```

## 📚 Component Documentation

### Button Component
```jsx
<Button variant="primary" size="lg" onClick={handleClick}>
  Click Me
</Button>
```

### Modal Component
```jsx
<Modal isOpen={isOpen} title="Title" onClose={handleClose}>
  Content here
</Modal>
```

### Toast Notification
```jsx
const { toast, showToast, hideToast } = useToast()
showToast('Success!', 'success')
```

## 🔐 Security Notes

- This is a demo application using mock authentication
- Implement proper security measures for production:
  - HTTPS only
  - Secure password hashing
  - JWT tokens with expiration
  - CORS configuration
  - Input validation and sanitization

## 📄 License

This project is provided as-is for educational and hackathon purposes.

## 🤝 Contributing

For enhancements or bug fixes:
1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request

## 📞 Support

For issues or questions, refer to the code comments and component documentation.

## 🎯 Future Enhancements

- [ ] Real backend API integration
- [ ] User profile pages
- [ ] Email notifications
- [ ] Advanced search filters
- [ ] Book recommendations
- [ ] Fine management module
- [ ] Inventory alerts
- [ ] Report generation
- [ ] Mobile app version
- [ ] WebSocket real-time updates

---

**Built with ❤️ for hackathons and modern library management**

Last Updated: February 2, 2026
"# Library-Management-System-1" 
