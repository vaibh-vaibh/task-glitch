# Task Glitch – Bug Fixes Challenge
This is a TypeScript + React (Vite) task management app used for a bug‑fixing assignment.  
The goal was to stabilize the app, fix hidden logic/UI issues, and make ROI‑based task prioritization reliable.[1]

## Tech Stack
- React + TypeScript (Vite)
- Material UI (MUI)
- Local state and derived metrics (no backend)
- CSV import/export for tasks[1]

## Fixed Bugs (Assignment Requirements)
The original app shipped with 5 intentional bugs affecting data loading, undo, sorting, dialogs, and ROI calculations.[1]

1. **Bug 1 – Double Fetch / Double Load**  
   - Problem: Task loading ran twice on app start, causing duplicate fetch and unnecessary renders.[1]
   - Fix: Added a guard so the load effect initializes tasks only once, even under React StrictMode.  

2. **Bug 2 – Undo Snackbar Restoring Wrong Task**  
   - Problem: After the snackbar closed, the next undo could restore an older deleted task instead of the latest one.[1]
   - Fix: Reset the “last deleted” state when the snackbar closes so undo only works for the current deletion window.  

3. **Bug 3 – Unstable Sorting (ROI Ties Flicker)**  
   - Problem: Tasks with the same ROI and priority kept changing order on re‑renders, causing a flickering list.[1]
   - Fix: Implemented a stable sort:  
     - Primary: ROI (higher first)  
     - Secondary: Priority weight (High > Medium > Low)  
     - Tie‑breaker: Title (A–Z), then id for deterministic order.  

4. **Bug 4 – Double Dialog Opening (View + Edit/Delete)**  
   - Problem: Clicking Edit/Delete on a row also triggered the row click handler, opening the View dialog together with Edit/Delete.[1]
   - Fix: Stopped event propagation on the action buttons so only the intended dialog opens.  

5. **Bug 5 – ROI Errors / Infinity / NaN**  
   - Problem: ROI calculation broke for invalid inputs (time = 0, invalid numbers), leading to Infinity / NaN values and inconsistent display.[1]
   - Fix:  
     - Added safe ROI validation in `logic.ts`.  
     - Treat invalid or zero time as “no ROI” (null), which is rendered as “N/A” in the UI.  
     - Metrics only use finite ROI values.  

## How to Run Locally

# install dependencies
npm install

# start dev server
npm run dev

Then open the printed URL (usually `http://localhost:5173`) in your browser.

## What You Can Do in the App
- Add, edit, and delete tasks
- View task details and notes in a dialog
- Sort by ROI and priority with stable ordering
- Use undo after delete via snackbar
- See summary metrics: total revenue, time efficiency, average ROI, performance grade
- Import and export tasks via CSV[1]

## Deployment
The app is deployed and publicly accessible:

- **Live Demo:** https://task-glitch-plum.vercel.app/
- **GitHub Repository:** https://github.com/vaibh-vaibh/task-glitch/
