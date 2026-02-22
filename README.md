# Student Registration Dashboard – Project Overview

## Project Purpose

The **Student Registration Dashboard** is a comprehensive web application designed to streamline the student registration process for educational institutions. It provides a dual-interface system: a user-friendly registration form for students and a secure admin dashboard for institutional staff to manage registrations efficiently.

The system aims to:
- **Simplify Registration**: Provide an intuitive, accessible interface for students to register.
- **Automate Communication**: Send automated confirmation emails to registrants.
- **Centralize Management**: Enable admins to view, search, filter, edit, and manage all student registrations.
- **Ensure Data Persistence**: Store all registrations securely using IndexedDB for client-side data persistence.
- **Enhance User Experience**: Offer dark mode, responsive design, and a premium UI/UX.

---

## 🌐 Live Demo
You can also view it online via GitHub Pages:  

👉 [Click here](https://srinath-69.github.io/Student-Registration-Dashboard/)

## Project Features

### For Students (Registration Page – `index.html`)

1. **Student Registration Form**
   - Collect essential student information: Name, Roll No., Branch, Year, and Email
   - Form validation for data accuracy
   - Branch selection with optional "Others" field for custom branches

2. **Automated Email Confirmation**
   - Send confirmation emails using EmailJS on successful registration
   - Confirmation includes student details for verification

3. **Dark Mode Toggle**
   - Switch between light and dark modes
   - Persistent user preference via localStorage

4. **Premium UI Design**
   - Peaceful, decorative background blobs for visual appeal
   - Clean, centered form layout
   - Responsive design for mobile and desktop

5. **Contact Us Footer**
   - Premium contact section with contact information
   - Embedded contact form that opens user's mail client for direct contact
   - Social media links
   - Current year dynamically displayed

---

### For Admins (Admin Dashboard – `admin.html`)

1. **Secure Login**
   - Password-protected admin access via security key
   - Simple authentication mechanism (hardcoded for demo; change in production)

2. **Student Data Management**
   - **View**: Display all registered students in a sortable, filterable table
   - **Search**: Search students by name, roll number, or email
   - **Filter**: Filter by branch and year of study
   - **Sort**: Click table headers to sort by any column (ascending/descending)
   - **Pagination**: Navigate through student records with Previous/Next buttons (10 records per page)

3. **Edit Student Records**
   - Click "Edit" button to open an inline edit panel
   - Edit fields: Name, Roll No., Branch, Year
   - Read-only email field (email cannot be edited)
   - Form validation ensures data integrity
   - Prevent duplicate roll numbers and emails
   - Save or cancel edits with real-time updates

4. **Delete Students**
   - Remove student records with confirmation dialog
   - Immediate data persistence

5. **Data Export/Import**
   - **Export to CSV**: Download student records in CSV format for spreadsheet applications
   - **Export to JSON**: Export all data as JSON for backup or transfer
   - **Import from JSON**: Restore or batch-import student records from a JSON file

6. **Dark Mode**
   - Toggle dark mode for comfortable admin work
   - Persistent preference via localStorage

---

## How It Works

### Data Flow

```
Student Registration Process:
1. Student fills registration form on index.html
2. Form validates data (name, roll no., branch, year, email)
3. Student data stored in IndexedDB (client-side database)
4. Automated confirmation email sent via EmailJS
5. Success message displayed to student

Admin Management Process:
1. Admin logs in with security key on admin.html
2. System loads all students from IndexedDB
3. Admin can search, filter, sort students in a table
4. Admin can edit student details (except email)
5. Admin can delete student records
6. Admin can export data (CSV/JSON) or import (JSON)
7. All changes persisted in IndexedDB
```

### Technology Stack

- **Frontend**: HTML5, CSS3, JavaScript (Vanilla JS)
- **Database**: IndexedDB (browser-based local storage)
- **Email Service**: EmailJS (automated email delivery)
- **Deployment**: Static HTML files (no server required for basic functionality)

### Key Components

| Component | Purpose | Location |
|-----------|---------|----------|
| Registration Form | Collect student data | `index.html` |
| Admin Dashboard | Manage registrations | `admin.html` |
| IndexedDB Database | Store student records | Client-side (automatic) |
| EmailJS Integration | Send confirmation emails | EmailJS service (external) |
| Contact Footer | Student contact channel | `index.html` footer |

---

## Architecture Overview

### Client-Side Architecture

```
┌─────────────────────────────────────┐
│   Student Registration Page         │
│        (index.html)                 │
│  ┌─────────────────────────────┐   │
│  │   Registration Form         │   │
│  │   - Validation              │   │
│  │   - EmailJS Integration     │   │
│  └─────────────────────────────┘   │
│  ┌─────────────────────────────┐   │
│  │   Contact Footer            │   │
│  │   - Contact Info            │   │
│  │   - Inline Contact Form     │   │
│  └─────────────────────────────┘   │
└─────────────────────────────────────┘
              ↓ (saves data)
     ┌────────────────────┐
     │   IndexedDB        │
     │  (StudentDB)       │
     │  - students        │
     │    (keyPath:       │
     │    rollno)         │
     └────────────────────┘
              ↓ (email trigger)
     ┌────────────────────┐
     │   EmailJS Service  │
     │  - Confirmation    │
     │    Email Template  │
     └────────────────────┘


┌─────────────────────────────────────┐
│   Admin Dashboard                   │
│        (admin.html)                 │
│  ┌─────────────────────────────┐   │
│  │   Login Form                │   │
│  │   - Security Key Auth       │   │
│  └─────────────────────────────┘   │
│  ┌─────────────────────────────┐   │
│  │   Student Table             │   │
│  │   - Search                  │   │
│  │   - Filter (Branch/Year)    │   │
│  │   - Sort (all columns)      │   │
│  │   - Pagination (10/page)    │   │
│  └─────────────────────────────┘   │
│  ┌─────────────────────────────┐   │
│  │   Edit Panel                │   │
│  │   - Edit: Name, Roll, etc.  │   │
│  │   - Read-only Email         │   │
│  │   - Validation              │   │
│  └─────────────────────────────┘   │
│  ┌─────────────────────────────┐   │
│  │   Export/Import Actions     │   │
│  │   - CSV Export              │   │
│  │   - JSON Export/Import      │   │
│  └─────────────────────────────┘   │
└─────────────────────────────────────┘
              ↓↑ (CRUD operations)
     ┌────────────────────┐
     │   IndexedDB        │
     │  (StudentDB)       │
     │  - students        │
     │    (keyPath:       │
     │    rollno)         │
     └────────────────────┘
```

---

## Use Cases

### Use Case 1: Student Self-Registration
- **Actor**: Student
- **Flow**: Student opens registration page → fills form → submits → receives confirmation email
- **Outcome**: Student record stored; confirmation sent

### Use Case 2: Admin Retrieves All Registrations
- **Actor**: Admin
- **Flow**: Admin logs in → views paginated student table → searches/filters as needed
- **Outcome**: Admin has searchable, filterable view of all registrations

### Use Case 3: Admin Edits Registration
- **Actor**: Admin
- **Flow**: Admin clicks Edit → modifies data in inline panel → clicks Save → data updates
- **Outcome**: Student record updated and persisted

### Use Case 4: Data Backup/Transfer
- **Actor**: Admin
- **Flow**: Admin exports data (CSV or JSON) → downloads file on computer
- **Outcome**: Data backup created for external storage or spreadsheet analysis

### Use Case 5: Bulk Import
- **Actor**: Admin
- **Flow**: Admin selects JSON file → imports data → system validates and stores
- **Outcome**: Multiple student records added in one action

---

## Installation & Setup

### Prerequisites
- Modern web browser (Chrome, Firefox, Safari, Edge)
- EmailJS account (for automated emails) – see `README.md` for setup

### Steps

1. **Clone or Download** the project files
2. **Configure EmailJS**:
   - Follow instructions in `README.md` to set up CustomJS account
   - Replace `publicKey`, `service_id`, and `template_id` in `index.html`
3. **Open in Browser**:
   - `index.html` – Student Registration page
   - `admin.html` – Admin Dashboard (login with `admin123` by default)
4. **Optional – Update Security Key**:
   - Edit `admin.html` script: change `SECURITY_KEY = 'admin123'` to a secure key

### Running Locally
Simply open the HTML files directly in your browser. No server setup required.

---

## Features in Detail

### 1. Form Validation
- **Name**: Minimum 3 characters required
- **Roll No.**: 6-11 alphanumeric characters; must be unique
- **Branch**: One of predefined branches or custom "Others"
- **Year**: One of 1st, 2nd, 3rd, 4th Year
- **Email**: Valid email format; must be unique

### 2. Dark Mode
- Toggle via bulb icon (top-right corner)
- Applied to entire page including forms, tables, footer
- Preference saved in browser's localStorage
- Label "darkmode" appears below the bulb for clarity

### 3. Pagination
- 10 student records displayed per page
- Navigation via Previous/Next buttons
- Page counter shows "Page X of Y"
- Buttons disabled at boundaries

### 4. Edit Panel
- Appears below the student table when Edit is clicked
- Smooth scroll into view for visibility
- Inline form with Name, Roll No., Branch, Year fields
- Email shown in read-only state
- Validation errors displayed in real-time
- Save/Cancel buttons for control

### 5. Data Persistence
- **IndexedDB** ensures data persists across browser sessions
- **Automatic**: No manual save required
- **Secure**: Data remains local; never sent to external servers (except emails)

---

## Security Considerations

 **Current Implementation (Demo)**:
- Security key is hardcoded in `admin.html` (for demo only)
- EmailJS public key is exposed in client-side code (acceptable for public key)
- No user authentication system in place

 **Recommended for Production**:
- Implement proper backend authentication
- Use environment variables for sensitive keys
- Implement role-based access control (RBAC)
- Add HTTPS encryption
- Implement audit logging
- Add rate limiting on API calls
- Hash and properly store passwords

---

## Browser Compatibility

| Browser | Support |
|---------|---------|
| Chrome |  Full |
| Firefox |  Full |
| Safari |  Full |
| Edge |  Full |
| Internet Explorer |  Not supported |

---

## Future Enhancements

1. **Backend API**: Move data to a server-side database (PostgreSQL, MongoDB)
2. **User Authentication**: Implement JWT-based auth with role management
3. **Multi-file Upload**: Allow students to upload documents (ID, proof, etc.)
4. **Email Templates**: Advanced email customization per branch/year
5. **Dashboard Analytics**: Charts showing registration trends, demographics
6. **Bulk Email**: Send notifications to groups of students
7. **QR Code**: Generate QR codes for student identification
8. **Mobile App**: React Native or Flutter app for mobile registration
9. **Payment Gateway**: Integrate for registration fees if applicable

---

## Support & Contact

For questions, issues, or feedback:
- **Email**: support@example.com
- **Phone**: +1 (234) 567-890
- Use the "Contact Us" footer on the registration page

---

## License & Disclaimer

This project is provided as-is for educational and institutional use. Modify as needed for your organization.

---
