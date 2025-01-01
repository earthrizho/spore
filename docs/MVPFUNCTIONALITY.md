Base Model Functionality (MVP)
The Base Model (MVP) focuses on core features to make Spore operational for managing estimates, projects, and tasks, while ensuring a functional user interface and backend.

1. Materials Management
Key Features:
Store materials in the materials collection in Firestore.
Fields: Name, unit cost, unit type, timestamps.
Dynamic material search during line item creation.
Add new materials to the database in real time.
UI:
Material search bar with autocomplete.
Form for adding new materials.
2. Labor Costing
Key Features:
Predefined labor costing methods: flat rate, hourly rate, per unit.
Custom formulas for labor costs (e.g., labor_cost = hours_worked * hourly_rate).
Input variable prompts for formulas (e.g., hours worked, workers).
Dynamic factors that impact labor costs (e.g., weather, accessibility).
UI:
Form to define labor costs with calculation methods and dynamic factors.
3. Line Item Creation
Key Features:
Create line items that include:
Name, description.
Selected materials with quantities and total costs.
Labor costing details (methods, variables, and factors).
Real-time calculation of material and labor costs.
Store line items in Firestore with metadata.
UI:
Line item creation form with dynamic inputs for materials and labor costs.
4. Estimate Creation
Key Features:
Create estimates by selecting multiple line items.
Input required variables for selected line items (e.g., hours worked, factor adjustments).
Automatically calculate total costs:
Material costs.
Labor costs (with factor adjustments).
Display a summary:
Total costs, labor vs. material breakdown, and line item details.
UI:
Estimate creation flow with dynamic input prompts and real-time summary display.
Database: Estimates stored in Firestore.
5. Dedicated Project Pages
Purpose: A central control center for each project.
Key Features:
Automatically generated when an estimate is approved.
Track and manage:
Tasks: View ordered tasks by sequencing labels defined in the estimate.
Weather: Display project-specific weather data.
Schedule: Adjust project schedules dynamically based on complexity, location, and dependencies with other projects.
Financial Tracking: Compare project costs vs. estimate budgets.
Material Management:
Track material delivery statuses.
Ensure materials arrive 1 day before their associated tasks.
Change Orders: Add and track approved change orders.
Documentation: Upload and manage design documents and project photos.
Provide a live project timeline.
UI:
Project dashboard displaying tasks, schedules, financials, and documents.
Real-time updates for task status and material delivery.
6. Basic Dashboard
Purpose: A global overview of the business.
Key Features:
Summarize:
Total estimates.
Active projects.
Notifications and tasks.
High-level KPIs (e.g., financial performance, task completion rate).
UI:
Widgets for quick access to core features (materials, estimates, projects, tasks).
7. Authentication
Firebase Authentication:
Secure user login using email/password or other methods.
Store user data and permissions for accessing estimates and projects.
Version 1.1 Enhancements
Version 1.1 builds on the MVP with advanced features to enhance functionality, user experience, and automation.

1. Advanced Dedicated Project Pages
Expanded Features:
Add task scheduling with advanced dependencies (e.g., Gantt chart view).
Dynamic Timeline Adjustments:
Account for delays due to weather or material shortages.
Notifications for project-specific updates:
Task progress or delays.
Material delivery changes.
Project status aggregation for the main dashboard.
2. Scheduling
Key Features:
Task scheduling with dependency-based sequencing (e.g., Task B starts after Task A).
Integration with weather forecasts for automatic schedule adjustments.
Visualize schedules using Gantt charts or calendar views.
3. Notifications
Key Features:
Real-time alerts for:
Task deadlines and status changes.
Estimate or project updates.
Email and SMS notifications for critical events.
4. Material Tracking
Key Features:
Track material orders, delivery statuses, and quantities.
Notifications for upcoming material needs.
Detailed material inventory management.
5. Advanced KPIs
Key Features:
Financial insights:
Actual costs vs. estimated budgets.
Task completion rates and project statuses.
Performance tracking for materials and labor usage.
6. Export Functionality
Key Features:
Export estimates and project reports to PDF, CSV, or Excel.
Include detailed summaries of material usage, labor costs, and tasks.
Comparison: Base Model vs. Version 1.1
Feature	Base Model (MVP)	Version 1.1
Materials Management	Basic material database and search.	Inventory tracking and detailed delivery statuses.
Labor Costing	Predefined/custom methods, dynamic factors.	Enhanced reporting and adjustments.
Line Item Creation	Core functionality with materials and labor.	Advanced adjustments and task-specific updates.
Estimate Creation	Material and labor cost breakdown.	Export to PDF, CSV, Excel.
Dedicated Project Pages	Core features for tracking tasks, financials.	Dynamic scheduling, notifications, and automation.
Scheduling	Not included.	Dependency-based scheduling and Gantt charts.
Notifications	Basic task and project updates.	Email and SMS alerts for critical events.
KPIs	Basic overview on the dashboard.	Advanced metrics and detailed insights.
Authentication	Firebase Authentication.	Enhanced user management features.
Export Functionality	Not included.	Full export functionality for estimates and reports.
Development Priority
Base Model (MVP):

Materials management.
Labor costing.
Line item creation.
Estimate generation.
Dedicated project pages (basic functionality).
Deploy and test the MVP.
Version 1.1:

Advanced project pages with scheduling and notifications.
Material tracking and advanced KPIs.
Export functionality.