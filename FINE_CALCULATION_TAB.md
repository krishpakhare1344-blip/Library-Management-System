# Fine Calculation Tab - User Dashboard

## Overview
A new "Fine Calculation" tab has been added to the user profile/dashboard page. This tab displays:
- Real-time fine calculations for overdue books
- User's blacklist status
- Detailed breakdown of each overdue book and its associated fine
- Fine calculation rules and guidelines

## Location
**File**: `src/pages/Profile.tsx`

## Features Added

### 1. **Summary Cards** (Top Section)
Three informative cards at the top:
- **Total Fine**: Sum of all fines for overdue books
- **Overdue Books**: Count of books with days overdue > 0
- **Account Status**: Shows "Active" or "Blacklisted" with icons

### 2. **Status Alerts**
- Shows alert box if user has overdue books
- Different styling for blacklisted vs. reminder status
- Helpful messages about returning books and paying fines

### 3. **Fine Calculation Rules**
Clear explanation of the fine structure:
- **Days 1-5**: No fine, daily reminder emails
- **Day 6+**: ₹10 per day fine
- **₹100 Cap**: Account blacklisted when fine reaches ₹100

### 4. **Books List**
Detailed table showing each issued book with:
- Book title
- Due date
- Days overdue (calculated automatically)
- Fine amount (₹)
- Status badge: "On Time", "Reminder", "Fine Due", or "Blacklisted"
- Color-coded rows for easy identification:
  - Green: On time
  - Yellow: Reminder (1-5 days overdue)
  - Orange: Fine due (6+ days overdue)
  - Red: Blacklisted (₹100 fine)

### 5. **Support Section**
Contact information for library administration assistance

## How Fine Calculation Works

### Automatic Calculation
```javascript
const dueDate = new Date(book.dueDate)
const today = new Date()
const daysOverdue = Math.floor((today.getTime() - dueDate.getTime()) / (1000 * 60 * 60 * 24))

// Fine Logic:
if (daysOverdue > 0 && daysOverdue <= 5) {
  fineAmount = 0
  status = 'reminder'
} else if (daysOverdue > 5) {
  fineAmount = Math.min((daysOverdue - 5) * 10, 100)
  status = fineAmount >= 100 ? 'blacklisted' : 'fine'
}
```

## Data Flow

1. User clicks on "Fine Calculation" tab
2. Component fetches user's issued books from API
3. For each book, calculates:
   - Days overdue
   - Fine amount
   - Current status
   - Whether reminder should be sent
4. Displays all calculated fines with visual indicators
5. Shows summary statistics at the top

## User Interface Elements

### Tab Navigation
```
Profile | Settings | Fine Calculation
```
New tab with AlertCircle icon

### Status Badges
- **Green**: On Time (0 fine)
- **Yellow**: Reminder (1-5 days, no fine)
- **Orange**: Fine Due (6+ days, ₹10/day)
- **Red**: Blacklisted (₹100 fine)

### Icons Used
- AlertCircle: Fine warning alerts
- CheckCircle: Account active status
- TrendingUp: Total fine display
- Clock: Overdue books count
- Bell: Support section

## Code Changes

### Imports Added
```tsx
import { AlertCircle, CheckCircle, Clock, TrendingUp } from 'lucide-react'
import { useEffect } from 'react'
```

### State Variables Added
```tsx
const [activeTab, setActiveTab] = useState<'profile' | 'settings' | 'fines'>('profile')
const [finesLoading, setFinesLoading] = useState(false)
const [issuedBooks, setIssuedBooks] = useState<any[]>([])
const [userFines, setUserFines] = useState<any[]>([])
```

### useEffect Hook
Fetches user's issued books and calculates fines when tab is selected:
- Only runs when `activeTab === 'fines'`
- Calculates days overdue automatically
- Determines fine status based on rules
- Updates display with fine information

## Responsive Design
- **Mobile**: Single column layout, stacked cards
- **Tablet**: Two-column layout for summary cards
- **Desktop**: Three-column layout with full details

## Dark Mode Support
All colors and styling fully support dark mode with appropriate Tailwind CSS classes

## Performance
- Loading states while fetching data
- Lazy loading only when tab is clicked
- Efficient calculation using client-side logic
- No additional server requests needed (uses existing mockApi)

## Integration with Backend
The tab is designed to work with the fine calculation system:
- Currently uses `mockApi.getIssuedBooks()`
- Can be connected to backend API: `GET /api/issued-books/user/:userId`
- Fine calculations match backend rules exactly
- Ready for integration with real fine payment API

## Future Enhancements
- Mark fine as paid button
- View payment history
- Download fine receipt
- Export fine report
- Real-time notification for blacklist status
- Integration with payment gateway

## Testing Checklist
- [x] Tab appears in profile navigation
- [x] Fine calculations match rules
- [x] Status badges display correctly
- [x] Color coding is appropriate
- [x] Responsive on mobile/tablet/desktop
- [x] Dark mode works properly
- [x] No TypeScript errors
- [x] Loading states functional
- [x] Empty state handled
- [x] Icons display correctly

## Browser Compatibility
Works on all modern browsers that support:
- ES6+ JavaScript
- CSS Grid and Flexbox
- localStorage (for user data)

## Accessibility
- Semantic HTML structure
- Proper heading hierarchy
- Color contrast meets WCAG standards
- Icons paired with text labels
- Clear status descriptions
