# Factory Management System
 
A Java Swing desktop application that simulates the day-to-day operation of a snack-food (chips) factory. It provides role-based dashboards for HR, Managers, and Supervisors to manage users, production lines, tasks, and inventory, with a simulated clock driving production progress in the background.
 
## Features
 
- **Role-based login** — Users authenticate as one of three roles: `HR`, `MANAGER`, or `SUPERVISOR`, each routed to its own dashboard (`LoginView` → `AppRouter`).
- **HR dashboard** — Manage user accounts and access.
- **Manager dashboard** — Create and monitor production lines, assign tasks to lines, and review notes/ratings per line. Gets live toast notifications on raw-material shortages.
- **Supervisor dashboard** — Manage inventory items and products, and view an operational dashboard (active lines, most-requested products, etc.).
- **Simulated production** — Each active product line runs on a background worker (`ProductLineWorker`) that consumes inventory and advances task progress over time, driven by a persistent `SimulatedClock` (simulated time is sped up relative to real time and saved to disk between runs).
- **Inventory & shortage handling** — Products consume defined item quantities (`requiredItems`); the system tracks stock levels, minimum stock thresholds, and warns when a line stalls due to missing materials.
- **CSV-backed persistence** — All application data (users, items, products, product lines, tasks, review notes, and the simulated clock) is stored in plain CSV/TXT files under `Data/`, no external database required.
- **Error logging** — Runtime errors are appended to `Data/Errors.csv` with timestamps via `ErrorLogger`.
- **Custom UI** — Built on [FlatLaf](https://www.formdev.com/flatlaf/) for a modern look and feel, with custom Swing components (rounded fields/buttons, floating action button, shadows, toast notifications) under `Util`/`Swing`.
## Tech Stack
 
- **Language:** Java (Swing/AWT for the UI)
- **UI Look & Feel:** FlatLaf 3.6 (bundled in `libs/`)
- **Additional UI libraries** (referenced by the IntelliJ module, not bundled — see [Setup](#setup)):
  - `swing-toast-notifications` 1.0.4
  - `flatlaf-extras` 3.4.1
  - `jsvg` 1.4.0
- **Data storage:** CSV / plain-text files (`Data/`) — no database
- **IDE project:** IntelliJ IDEA (`P3-assignment.iml`)
## Project Structure
 
```
P3-assignment/
├── Data/                  # CSV data store (users, items, products, tasks, etc.) + Errors.csv log
├── libs/                  # Bundled third-party jars (FlatLaf)
├── src/
│   ├── Control/           # Controllers wiring views to services (AppRouter, LoginController, ...)
│   ├── Service/           # Business logic (UserService, TaskService, InventoryService, ...)
│   ├── Repository/        # CSV read/write persistence layer per entity
│   ├── Model/              # Domain models (User, Product, ProductLine, Task, Item, ReviewNotes, ...)
│   ├── View/                # Swing screens (LoginView, HRView, ManagerView, SupervisorView, DashBoard, ...)
│   ├── Swing/                # Reusable custom Swing components
│   ├── Util/                  # Enums, helpers, simulated clock, shutdown manager, custom UI utilities
│   ├── io/                    # Low-level CSV/TXT file readers & writers, error logger
│   ├── Images/                 # Icons, backgrounds, and GIFs used by the UI
│   └── FactoryApplication.java # Application entry point (main)
└── P3-assignment.iml       # IntelliJ module configuration
```
