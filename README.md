<div align="center">
<img width="1200" height="475" alt="GHBanner" src="https://github.com/user-attachments/assets/0aa67016-6eaf-458a-adb2-6e31a0763ed6" />
</div>

View your app in AI Studio: https://ai.studio/apps/drive/1O59WKKQiqaE8f2TE4YxfQtsjaThCeTSd

# 114th Signal Company Training Calendar

This is a web-based training calendar designed to provide a shared, consistent view of the training schedule for all members of the unit.

## About This Application

This application serves as the single source of truth for the company's training schedule. It's built as a static web application that reads from a central, shared database file.

### Key Features

*   **Shared Data Model**: Utilizes an in-browser SQLite database (`sql.js`) to load a shared `training_calendar.db` file. Every user sees the exact same schedule, ensuring consistency.
*   **Read-Only Interface**: The user interface is strictly for viewing the schedule. This prevents accidental changes and ensures data integrity. All schedule updates are managed centrally.
*   **Multiple Views**: Toggle between **Year**, **Month**, and **Week** views to get a high-level overview or a detailed daily plan.
*   **Search Functionality**: Quickly find specific training events by searching for keywords, METL tasks, or shift leads.
*   **Data Export**: Export the calendar data for a selected date range into **JSON** or **CSV** format for external use.
*   **Printable View**: Generate a clean, formatted printout of the schedule for any given date range.
*   **Responsive Design**: Fully functional on desktops, tablets, and mobile devices.

### Important Disclaimer

This is an **unofficial tool** and must be treated as such.

**DO NOT** enter any Classified, Controlled Unclassified Information (CUI), or Personally Identifiable Information (PII) into this application or its underlying database file.

## Managing the Schedule

Because the live application is **read-only**, the training schedule cannot be modified through the web interface. Updates must be made by modifying the database file directly and deploying the changes.

To update the schedule:
1.  **Obtain the `training_calendar.db` file** from the repository.
2.  **Use a SQLite database editor** (such as [DB Browser for SQLite](https://sqlitebrowser.org/)) to open and modify the file. You can add, remove, or update events as needed.
3.  **Commit and push the updated `training_calendar.db` file** to the `main` branch of the repository.
4.  The CI/CD pipeline (GitHub Actions or GitLab CI) will automatically deploy the new version of the database, and the changes will be live for all users.

## Run Locally

You can run a local instance of this application to test changes before deployment.

**Prerequisites:** [Node.js](https://nodejs.org/) installed on your system.

1.  **Clone the repository:**
    ```bash
    git clone <repository-url>
    cd <repository-directory>
    ```
2.  **Install dependencies:**
    ```bash
    npm install
    ```
3.  **Build the application:**
    This command uses `esbuild` to create the `bundle.js` file.
    ```bash
    npm run build
    ```
4.  **Serve the application:**
    Since this is a static site, you need a simple local web server. The easiest way is using the `serve` package.
    ```bash
    npx serve
    ```
    This will start a local server, and you can view the application in your browser at the URL provided (usually `http://localhost:3000`).

## Deployment

Deployment is handled automatically by the CI/CD pipeline configured in the repository (`.github/workflows/deploy.yml` for GitHub Actions or `.gitlab-ci.yml` for GitLab CI).

Every push to the `main` branch will trigger a workflow that:
1.  Installs dependencies.
2.  Builds the application (`npm run build`).
3.  Deploys the static files (`index.html`, `index.css`, `bundle.js`, and `training_calendar.db`) to the web host (GitHub Pages or GitLab Pages).
