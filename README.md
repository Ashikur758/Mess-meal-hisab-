# Mess Meal Hisab (মিল হিসাব)

A simple, lightweight, and user-friendly web application for managing mess meals, member contributions, daily expenses, and automatic meal rate calculations.

Mess Meal Hisab provides a centralized platform where all members can view records, while only the authorized manager can add, update, or delete information.

**Built with HTML, CSS, Vanilla JavaScript, Firebase Firestore, Firebase Authentication, and Netlify.**

---

## 🌐 Live Demo

**Website:** https://messashikur.netlify.app/

---

## 📖 Overview

Managing a shared mess requires maintaining accurate records of daily meals, member payments, grocery expenses, and monthly financial calculations.

**Mess Meal Hisab** simplifies this process by replacing traditional manual record-keeping with an organized digital management system.

The application features a clean, accessible, and user-friendly interface designed for everyday mess management.

## 📸 Screenshots

Explore the application's interface through the following screenshots.

### Application Dashboard
![Application Dashboard](mess-hishab_web/image%201.png)

### Meal Management
![Meal Management](mess-hishab_web/iamge%203.jpeg)

### Member Meal Details
![Member Meal Details](mess-hishab_web/image%202.jpeg)

### Individual Member Meal Details
![Individual Member Meal Details](mess-hishab_web/image%206.png)

### Expense Management
![Expense Management](mess-hishab_web/iamge%204.jpeg)

### Meal Rate Calculation
![Meal Rate Calculation](mess-hishab_web/iamge%205..jpeg)

---

## ✨ Key Features

### 1. Meal Management

- View all registered mess members.
- Add new members using the `+` button.
- Remove members with a confirmation dialog.
- Open individual meal records by clicking a member's name.
- Track daily meals using interactive checkboxes.
- Manage three meal categories:
  - Morning
  - Noon
  - Night
- Automatically generate a 30-day meal schedule based on a common starting date.
- Display dates with their corresponding weekdays.
- Automatically calculate individual meal counts and overall totals.

### 2. Member Collections

- Automatically synchronize member names with the Meal Management section.
- Record payments received from individual members.
- Add new payments using the `+` button.
- Display each member's total collected amount.
- Edit payment totals using the edit (✎) button.
- Maintain an organized overview of member contributions.

### 3. Expense Management

- Record daily mess expenses.
- Store the following information:
  - Bazar Person
  - Purchased Items
  - Expense Date
  - Amount
- Add new expense records through an entry form.
- Automatically calculate and display total expenses.

### 4. Meal Rate Calculation

Automatically calculate the meal rate using the total expenses and total meals of all registered members.

**Formula:**

```text
Meal Rate = Total Expenses / Total Meals
```

This provides an easy way to determine the cost of each meal.

### 5. Khala's Money Management

- Automatically retrieve member names from the Meal Management section.
- Record the amount assigned to each member.
- Allow the manager to update individual amounts.
- Maintain a centralized record of Khala's payments.

### 6. Authentication and Access Control

The application supports two types of access:

| User Type | Permissions |
|---|---|
| General Visitor | View all available records |
| Manager | View, add, edit, and delete records |

Additional authentication features:

- No login is required for general visitors.
- The manager authenticates using an email address and password.
- Firebase Authentication handles manager login.
- Firestore Security Rules enforce write permissions at the database level.

### 7. Demo Mode

The application supports a local demo mode when Firebase has not been configured.

- Runs directly in a web browser.
- Uses browser `localStorage` for data persistence.
- Allows users to explore and test the application.
- Demo data remains local to the browser and is not synchronized with Firebase.

---

## 🛠️ Technology Stack

| Technology | Purpose |
|---|---|
| HTML5 | Application structure |
| CSS3 | Styling and responsive interface |
| JavaScript (Vanilla) | Application logic and functionality |
| Firebase Firestore | Cloud database and data storage |
| Firebase Authentication | Manager authentication |
| Netlify | Static website hosting |
| localStorage | Local demo-mode data persistence |

**Architecture:** Single-page web application (SPA) with no build process or additional frontend framework.

---

## 📂 Project Structure

```text
mess-meal-hisab/
│
├── index.html
├── README.md
│
└── mess-hishab_web/
    ├── image 1.png
    ├── iamge 3.jpeg
    ├── image 2.jpeg
    ├── image 6.png
    ├── iamge 4.jpeg
    └── iamge 5..jpeg
```

The entire frontend application is implemented in a single `index.html` file, making the project lightweight and easy to deploy.

---

## 🚀 Installation and Configuration

### Prerequisites

Before deploying the application, you need:

- A Google account.
- A Firebase project.
- A Netlify account.
- A modern web browser.

### Step 1: Create a Firebase Project

1. Visit the [Firebase Console](https://console.firebase.google.com/).
2. Create a new Firebase project.
3. Navigate to **Build → Firestore Database**.
4. Create a Firestore database.
5. Navigate to **Build → Authentication**.
6. Enable the **Email/Password** sign-in provider.
7. Under Authentication → Users, create an account for the authorized manager.
8. Navigate to Project Settings → General.
9. Register a new Web App and copy the Firebase configuration.

### Step 2: Configure Firestore Security Rules

Navigate to:

**Firebase Console → Firestore Database → Rules**

Add the following security rules and replace the example email with the manager's actual email address.

```javascript
rules_version = '2';

service cloud.firestore {
  match /databases/{database}/documents {

    match /{document=**} {

      // Public read access
      allow read: if true;

      // Only the authorized manager can write data
      allow write: if request.auth != null
                   && request.auth.token.email == "manager@example.com";
    }
  }
}
```

**Security Note:** These rules enforce access permissions at the database level. Restricting access through frontend buttons alone does not provide sufficient security.

### Step 3: Configure Firebase

Open `index.html` and locate the `firebaseConfig` object.

Replace the placeholder values with your Firebase Web App configuration.

```javascript
const firebaseConfig = {
  apiKey: "YOUR_API_KEY",
  authDomain: "YOUR_PROJECT.firebaseapp.com",
  projectId: "YOUR_PROJECT_ID",
  appId: "YOUR_APP_ID"
};
```

The Firebase Web configuration is intended for client-side use. Database access must be protected through properly configured Firebase Security Rules.

### Step 4: Deploy to Netlify

You can deploy the application using either of the following methods.

**Option A: Manual Deployment**

1. Visit [Netlify](https://www.netlify.com/).
2. Navigate to Sites.
3. Select **Add new site → Deploy manually**.
4. Drag and drop the project folder.
5. Wait for the deployment to complete.

**Option B: GitHub Integration**

1. Push the project repository to GitHub.
2. Log in to Netlify.
3. Select **Add new site → Import from Git**.
4. Connect your GitHub account.
5. Select the project repository.
6. Configure the deployment settings:
   - Build Command: Leave empty.
   - Publish Directory: `/`
7. Deploy the site.

No build process is required.

### Step 5: Configure Authorized Domains

To enable manager authentication on your deployed website:

1. Open Firebase Console.
2. Navigate to Authentication → Settings.
3. Find the Authorized Domains section.
4. Add your Netlify domain.

Example:

```text
messashikur.netlify.app
```

The manager can now log in using the configured email and password.

---

## 🔄 Application Workflow

1. Open the website to access the application.
2. Navigate to Meal Management and configure the mess starting date.
3. Add all mess members.
4. Open each member's individual page and record daily meals.
5. Navigate to Member Collections to record contributions.
6. Navigate to Expense Management to record grocery and other expenses.
7. Update individual amounts in Khala's Money Management.
8. Visit Meal Rate Calculation to view the automatically calculated meal rate.

### Monthly Data Management

Setting a new starting date initiates a new monthly accounting period.

Before applying the new date:

- The application displays a confirmation dialog.
- Previous meal records are cleared.
- Previous collection records are cleared.
- Previous expense records are cleared.
- Previous Khala's money records are cleared.
- Existing member names are preserved.

**Important:** The current implementation uses a single data document. Changing the starting date clears the previous period's records. Export or back up your data before starting a new period.

---

## 🗄️ Database Structure

The application stores its main data in a single Cloud Firestore document:

```text
Collection: mess
Document: data
```

### Example Data Structure

```json
{
  "startDate": "2026-11-06",

  "members": [
    {
      "id": "abc1",
      "name": "Rahim"
    }
  ],

  "meals": {
    "abc1": {
      "2026-11-06": [0, 1, 1]
    }
  },

  "collected": {
    "abc1": 1500
  },

  "expenses": [
    {
      "id": "x1",
      "who": "Rahim",
      "what": "Rice",
      "date": "2026-11-07",
      "amount": 800
    }
  ],

  "khala": {
    "abc1": 200
  }
}
```

### Data Field Description

| Field | Description |
|---|---|
| `startDate` | Starting date of the mess accounting period |
| `members` | List of registered mess members |
| `meals` | Individual daily meal records |
| `collected` | Total money collected from each member |
| `expenses` | List of mess expense records |
| `khala` | Individual Khala's money records |

### Meal Data Representation

Each day's meal record is stored as an array:

```javascript
[Morning, Noon, Night]
```

For example:

```javascript
[0, 1, 1]
```

This means:

- Morning: No meal
- Noon: Meal taken
- Night: Meal taken

Here, `1` represents a meal taken and `0` represents no meal.

---

## ⚠️ Important Notes and Limitations

- Firebase must be configured to enable cloud-based data synchronization.
- Without Firebase configuration, the application operates in local demo mode.
- Demo-mode data is stored only in the current browser's `localStorage`.
- Only one manager account is intended in the current implementation.
- Simultaneous edits by multiple managers may overwrite each other because the application uses a single Firestore document.
- Starting a new accounting period clears previous monthly records.
- The current data structure is designed for a small mess rather than a large-scale accounting system.

---

## 🔮 Future Improvements

Potential enhancements for future versions include:

- Monthly data archiving and historical records.
- PDF and Excel report generation.
- Individual member account summaries.
- Automated monthly financial reports.
- Improved data backup and restoration.
- Multiple manager support.
- Real-time synchronization and conflict handling.
- Member-wise meal and payment balance calculations.

---

## 📄 License

This project is developed for educational and practical mess management purposes.

---

## 👨‍💻 Author

**Ashikur Rahman Ashik**

- GitHub: [@Ashikur758](https://github.com/Ashikur758)
- Project: [Mess Meal Hisab](https://messashikur.netlify.app/)

**If you find this project useful, consider giving it a ⭐ on GitHub!**
