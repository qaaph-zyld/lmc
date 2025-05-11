# White-Label Open Source LMS Project

This project aims to implement a white-label Learning Management System (LMS) based on Open edX, following the White-Label LMS Architecture Blueprint.

## Project Goals

- Deploy a fully functional Open edX instance.
- Implement white-labeling capabilities for custom branding.
- Establish a scalable infrastructure using Docker and Kubernetes.
- Automate deployment and operational tasks.

## Architecture

Key architecture decisions are documented in the `docs/adr` directory.
- **ADR-001:** Defines the repository structure.
- **ADR-002:** Specifies the use of Tutor for Open edX containerization.

Refer to `project_architecture.md` for the full system architecture blueprint.

## Development

- **Development Journal:** See `development_journal.md` for ongoing progress and status.
- **Checking Protocol:** See `checking_protocol.md` for compliance verification.
- **Error Prevention:** See `error_prevention_mechanism.md` for AI coder guidelines.

## Development with GitHub Codespaces

This project is configured to use GitHub Codespaces for a consistent and cloud-based development environment, eliminating the need for local Docker or Tutor installation.

### Launching the Codespace

1.  Navigate to the main page of the repository on GitHub.
2.  Click the "Code" button.
3.  Select the "Codespaces" tab.
4.  Click "Create codespace on main" (or your current branch).

GitHub will then set up your Codespace. This might take a few minutes the first time.

### Automatic Initial Setup

Once the Codespace is built and you connect to it (e.g., via VS Code in the browser or desktop), the configuration in `.devcontainer/devcontainer.json` automatically performs the following:

*   Sets up Docker-in-Docker (to allow Tutor to run its containers).
*   Installs Python 3.10.
*   Creates a Python virtual environment specifically for Tutor at `~/tutor_venv`.
*   Installs the latest version of Tutor and all its extras (`tutor[full]`) into this virtual environment.
*   Adds a line to `~/.bashrc` to automatically activate the `~/tutor_venv` in new terminal sessions.
*   Adds an alias for `tutor` to point to `~/tutor_venv/bin/tutor`.
*   Displays a welcome message with key information when a new terminal opens.

You can monitor the progress of this `postCreateCommand` in the terminal that appears when the Codespace first loads.

### First-Time Open edX Setup

After the automatic `postCreateCommand` completes (you'll see the welcome message and instructions in your terminal):

1.  **Open a new terminal** in VS Code within the Codespace (if one isn't already open or if you want a clean one).
2.  The Tutor virtual environment (`~/tutor_venv`) should be automatically activated.
3.  Run the Tutor quickstart command. This command will build the Docker images for Open edX, configure it, and start it. This process will take a significant amount of time (potentially 20-40 minutes or more depending on system resources allocated by Codespaces).
    ```bash
    tutor local quickstart
    ```
    Follow any prompts. For the LDomain, you can use `local.overhang.io` if you don't have a specific domain in mind for this initial setup.

### Accessing Open edX

Once `tutor local quickstart` (or `tutor local start`) is complete:

*   **LMS (Learning Management System):** GitHub Codespaces automatically forwards port `8000`. You should see a notification in VS Code, or you can go to the "Ports" tab in VS Code to find the forwarded URL. It will typically be something like `https://<your-codespace-name>-8000.app.github.dev`.
*   **Studio (Course Management System):** GitHub Codespaces automatically forwards port `8001`. Similar to the LMS, find the forwarded URL in the "Ports" tab. It will typically be `https://<your-codespace-name>-8001.app.github.dev`.

Default login credentials after `quickstart` are usually:
*   Username: `admin`
*   Password: `admin` (or as specified during `quickstart` if prompted)

### Subsequent Starts and Stops

*   **To start Open edX (after the initial `quickstart`):**
    ```bash
    tutor local start
    ```
*   **To stop Open edX:**
    ```bash
    tutor local stop
    ```
*   **To view logs:**
    ```bash
    tutor local logs -f   # For all services
    tutor local logs -f lms # For LMS only
    tutor local logs -f cms # For Studio only
    ```

### Tutor Virtual Environment

The Tutor installation is contained within the `~/tutor_venv` Python virtual environment.
*   This environment is automatically activated when you open a new terminal in Codespaces.
*   If you need to manually activate it in a script or a non-standard shell session: `source ~/tutor_venv/bin/activate`
*   The `tutor` command is directly available due to the alias and the venv activation.

### Troubleshooting

*   If Docker commands fail, ensure the Docker-in-Docker feature started correctly. Check the `postCreateCommand` logs.
*   If Tutor commands are not found, ensure `~/tutor_venv/bin` is in your `PATH` or that the venv is active (`which tutor` should point to the venv).

This setup provides a fully functional Open edX development environment managed by Tutor, all within GitHub Codespaces.

## Getting Started

(Instructions for setting up the development environment and running the LMS will be added here as the project progresses.)
