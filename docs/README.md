Spore: Documentation

Spore: Documentation
Project Overview
Spore is a landscape business management dashboard designed to streamline operations for businesses. It provides tools to manage estimates, projects, tasks, notifications, and business KPIs, all within a modular, scalable, and maintainable architecture.

Core Features
1. Estimates
Create and manage project estimates with:
Materials (costs, quantities).
Labor costs (hours, rates).
Dynamic factors (e.g., complexity, weather).
Store estimates in Firebase for real-time access.
Example Use Case: Generate detailed project cost breakdowns.
2. Project Management
Track projects with:
Timelines and statuses (e.g., Not Started, In Progress, Completed).
Task sequencing based on dependencies.
Link projects to their corresponding estimates.
Manage project-level documents and photos.
3. Tasks (To-Do Lists)
Create and manage tasks with:
Deadlines and priority levels.
Progress tracking (e.g., Pending, Completed).
Organize tasks by project for streamlined management.
4. Notifications
Real-time alerts for:
Task deadlines.
Project status updates.
Overdue tasks or urgent changes.
Notifications can be marked as read or dismissed.
5. Business KPIs
Display key metrics:
Total estimates created.
Task completion rates.
Active and completed projects.
Financial performance comparisons.
Technologies and Tools
Languages and Frameworks
React: Frontend framework for building the user interface.
JavaScript (ES6): Core language for business logic and Firebase interactions.
CSS/SCSS: Styling framework for the application.
HTML: Structure for rendering the app.
Backend
Firebase:
Firestore: Real-time NoSQL database for storing and managing application data.
Firebase Authentication: Secure login for users.
Firebase Storage: Upload and manage documents, photos, and files.
Testing
Jest: Testing framework for unit and integration tests.
React Testing Library: For UI interaction tests.
Firebase Mocks: Simulate Firebase interactions during tests.
Version Control
GitHub:
Main Branch: Stable, production-ready code.
Develop Branch: Staging for integrating features.
Feature Branches: Separate branches for new features (e.g., feature/estimating-module).
Architecture
Directory Structure
The project is modular to ensure scalability and maintainability:

bash
Copy code
/root
  /src                    # Source code
    /api                  # Firebase and external API integrations
      firebase.js         # Firebase setup and CRUD helpers
    /components           # Reusable UI components
      /common             # Common components (e.g., Button, Modal)
      /dashboard          # Dashboard components
      /features           # Feature-specific components
    /features             # Core feature logic
      /estimating         # Estimate-related logic and state
      /projects           # Project management logic
      /tasks              # Task management logic
      /notifications      # Notification logic
      /kpi                # KPI calculation logic
    /hooks                # Custom React hooks (e.g., useAuth, useFirestore)
    /services             # Shared utilities and helpers
    /styles               # Global and component-specific styles
    App.js                # Main app component
    index.js              # React DOM entry point
  /public                 # Static assets (HTML, images, etc.)
    index.html            # Main HTML file
  /tests                  # Unit and integration tests
    /unit                 # Unit tests for components and logic
    /integration          # Integration tests for feature interactions
    /mocks                # Mock files for Firebase and external services
  /config                 # Configuration files
    firebase.json         # Firebase configuration
    database.rules.json   # Firestore security rules
  /docs                   # Documentation for developers
  package.json            # Project dependencies
  .gitignore              # Git ignore rules
Development Workflow
Setup:

Initialize Firebase and configure Firestore collections:
estimates, projects, tasks, notifications.
Configure Firebase Authentication and Storage.
Core Development:

Build the following features first:
Estimating Module: CRUD operations for estimates.
Project Management: Link projects to estimates and track progress.
Tasks: Create, update, and manage task lists.
Notifications: Real-time alerts for users.
KPIs: Basic metrics displayed on the dashboard.
Testing:

Use Jest and React Testing Library for unit and integration tests.
Mock Firebase services in /tests/mocks to simulate interactions.
Deployment:

Use Firebase Hosting for deployment.
Example command:
bash
Copy code
firebase deploy --only hosting
GitHub Branching:

Work on features in separate branches (e.g., feature/estimating-module).
Merge branches into develop after testing.
API Examples
Firebase CRUD Helpers
File: /src/api/firebase.js

javascript
Copy code
import { getFirestore, doc, setDoc, getDoc, updateDoc, deleteDoc } from "firebase/firestore";

const db = getFirestore();

export const createDocument = async (collection, data) => {
  const docRef = doc(db, collection, data.id || Date.now().toString());
  await setDoc(docRef, data);
};

export const getDocument = async (collection, id) => {
  const docRef = doc(db, collection, id);
  const snapshot = await getDoc(docRef);
  return snapshot.exists() ? snapshot.data() : null;
};

export const updateDocument = async (collection, id, data) => {
  const docRef = doc(db, collection, id);
  await updateDoc(docRef, data);
};

export const deleteDocument = async (collection, id) => {
  const docRef = doc(db, collection, id);
  await deleteDoc(docRef);
};
Development Best Practices
Modularity:

Separate logic into distinct modules (/src/features) for scalability.
Reusability:

Create reusable components (/src/components/common) for shared UI elements.
State Management:

Use @reduxjs/toolkit for efficient global state management.
Code Quality:

Use ESLint and Prettier for consistent coding standards.
Testing:

Write unit tests for individual components and integration tests for feature interactions.
Future Enhancements
Scheduling:
Add dependency-based task sequencing with timeline visualizations.
Material Tracking:
Track material orders, delivery statuses, and quantities.
Advanced Notifications:
Enable email and SMS alerts.
Centralized Dashboard:
Aggregate business KPIs, project statuses, and notifications into a single view


Spore:Comprehensive Documentation
Project Overview
Spore is a landscape business management dashboard designed to provide comprehensive tools for creating detailed estimates, managing projects, and tracking key metrics. It leverages a modular React-based front end and Firebase for real-time backend capabilities.

Key Features
1. Materials Management
Materials Database:

Fields include:
Material Name
Unit Cost
Unit Type (e.g., per square foot, per gallon)
Metadata (timestamps, category).
Dynamically searchable during line item creation.
New materials can be added to the database in real time.
Materials are stored in the materials collection in Firestore.
Line Item Integration:

Materials are selected from the database during line item creation.
Users input quantities, and the app calculates the total material cost (unit cost × quantity).
Material details (name, unit cost, quantity, total cost) are stored within the line item.
2. Labor Costing
Calculation Methods:

Predefined methods:
Flat rate.
Hourly rate.
Per unit.
Custom methods:
Users define formulas (e.g., labor_cost = hours_worked × hourly_rate).
Variable Inputs:

Variables (e.g., hours_worked, workers) are required during line item creation.
Variables are described for user understanding (e.g., "Number of hours worked").
Dynamic Factors:

Factors that impact labor costs (e.g., accessibility, weather, complexity).
Factor properties:
Name (e.g., "Weather Factor").
Default Value (e.g., 1 for neutral impact).
Impact Type (multiplier or percentage adjustment).
Factors are adjustable during estimate creation.
3. Line Item Creation and Management
Line Item Details:

Includes:
Name and description.
List of materials (quantities, total costs).
Labor costs:
Calculation method.
Variables and factors.
Total labor cost.
Metadata (timestamps, categories).
Firestore Integration:

Line items are stored in the line_items collection with details for materials, labor, and metadata.
Editing and Deletion:

Users can edit or delete line items, and Firestore updates in real time.
4. Estimate Creation
Dynamic Estimates:

Users select line items for inclusion in an estimate.
Required variables (e.g., hours worked, workers) are prompted during estimate creation.
Total costs are calculated dynamically based on:
Material costs.
Labor costs (including factor adjustments).
Summary and Breakdown:

Estimate details include:
Total Costs.
Breakdown of material vs. labor costs.
Individual line item details.
Export Options:

Export estimates to formats such as PDF, CSV, or Excel.
Firestore Database Schema
Materials Collection
Stores information about available materials.

json
Copy code
{
  "materials": {
    "material_id_1": {
      "name": "Drywall Sheet",
      "unit_cost": 10.00,
      "unit_type": "per sheet",
      "created_at": "2024-12-31T12:00:00Z",
      "updated_at": "2024-12-31T13:00:00Z"
    },
    "material_id_2": {
      "name": "Paint (5-gallon)",
      "unit_cost": 100.00,
      "unit_type": "per bucket",
      "created_at": "2024-12-31T12:00:00Z",
      "updated_at": "2024-12-31T13:00:00Z"
    }
  }
}
Line Items Collection
Stores details for each line item, including materials, labor, and metadata.

json
Copy code
{
  "line_items": {
    "line_item_id_1": {
      "name": "Drywall Installation",
      "materials": {
        "material_id_1": {
          "name": "Drywall Sheet",
          "unit_cost": 10.00,
          "quantity": 50,
          "total_cost": 500.00
        }
      },
      "labor": {
        "calculation_method": "hourly_rate",
        "variables": {
          "hours_worked": { "type": "number", "description": "Number of hours worked" },
          "workers": { "type": "number", "description": "Number of workers" }
        },
        "factors": {
          "accessibility_factor": { "default_value": 1.2, "impact_type": "multiplier" },
          "weather_factor": { "default_value": 1, "impact_type": "multiplier" }
        }
      },
      "labor_costs": 300.00,
      "description": "Includes drywall and installation labor.",
      "created_at": "2024-12-31T12:00:00Z",
      "updated_at": "2024-12-31T13:00:00Z"
    }
  }
}
Development Steps
Frontend (React):
UI for Materials Management:

Implement material search and selection.
Build a form for adding new materials.
Line Item Creation:

Develop forms for:
Adding materials and labor.
Inputting variables and factors.
Dynamically calculate costs in the UI.
Estimate Creation:

Build a flow for:
Selecting line items.
Inputting required variables.
Display real-time cost calculations.
Export Functionality:

Use libraries like jspdf or sheetjs for exporting estimates to PDF, CSV, and Excel.
Backend (Firestore Integration):
Database Setup:

Create collections for materials, line_items, and estimates.
CRUD Operations:

Implement helper functions in /src/api/firebase.js for interacting with Firestore:
javascript
Copy code
export const createDocument = async (collection, data) => { /*...*/ };
export const getDocument = async (collection, id) => { /*...*/ };
Dynamic Data Updates:

Use Firestore listeners to update materials, line items, and estimates in real time.
Testing:
Unit Tests:
Test labor cost calculations and dynamic factor adjustments.
Integration Tests:
Verify end-to-end functionality for line item creation and estimate generation.
Mocking Firebase:
Use @firebase/testing to simulate Firestore interactions during tests.