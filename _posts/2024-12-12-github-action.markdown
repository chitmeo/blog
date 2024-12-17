---
layout: post
title:  "Github action tutorial"
date:   2024-12-12 17:09:25 +0700
categories: github action
---

# Understanding GitHub Actions
## Overview
GitHub Actions is a continuous integration and continuous delivery (CI/CD) platform that allows you to automate your build, test, and deployment pipeline.

GitHub provides Linux, Windows, and macOS virtual machines to run your workflows, or you can host your own self-hosted runners in your own data center or cloud infrastructure.
## The components of GitHub Actions
### Workflow
Definition: A workflow is an automated process that you set up in your repository. It can be triggered by an event, run on a schedule, or be manually triggered.

File Location: Workflows are defined in YAML files stored in the .github/workflows directory of your repository.

Structure: A workflow can contain one or more jobs, and each job contains a series of steps.

### Event
Definition: An event is an activity that triggers a workflow. Examples include pushes to a repository, the creation of a pull request, or the occurrence of a schedule event.

Types: Common event types are push, pull_request, schedule, workflow_dispatch (manual trigger), etc.

Configuration: In the workflow YAML file, you define events under the on keyword.

### Runner
Definition: A runner is a machine that runs the jobs in a workflow. GitHub provides hosted runners with different operating systems, or you can use self-hosted runners.

Types:

GitHub-hosted runners: Managed by GitHub and automatically scale with your usage.

Self-hosted runners: Machines that you manage and register with GitHub Actions, providing more control and customization.

### Job
Definition: A job is a set of steps that execute on the same runner. Each job in a workflow is isolated from the others.

Dependencies: Jobs can run sequentially or in parallel. You can set dependencies between jobs using the needs keyword.

Configuration: Jobs are defined under the jobs keyword in the workflow YAML file.

### Step
Definition: A step is an individual task within a job. Steps are executed sequentially in the order they're defined.

Actions: Steps can either run commands directly in the runner environment or use actions (reusable pieces of code).

Configuration: Steps are defined under the steps keyword within a job in the workflow YAML file.

# Hosting Your Own Runners on Windows OS

This guide walks you through setting up a self-hosted GitHub Actions runner on a Windows OS.

## Prerequisites

- A GitHub account.
- A Windows machine with:
  - Windows 10 or 11 (Pro, Enterprise, or Education recommended).
  - At least 4 GB of RAM and sufficient disk space.
- Administrative privileges on the Windows machine.
- .NET Framework 4.6 or higher installed.

## Step 1: Create a Runner in GitHub

1. Navigate to your repository or organization on GitHub.
2. Go to **Settings** > **Actions** > **Runners**.
3. Click **New self-hosted runner**.
4. Select **Windows** as the operating system.
5. Note the URL and token generated; you'll use them later.

## Step 2: Download and Configure the Runner

1. Open a web browser on your Windows machine and navigate to the URL provided in Step 1.
2. Download the runner package (e.g., `actions-runner-win-x64-<version>.zip`).
3. Extract the ZIP file to a directory (e.g., `C:\actions-runner`).

### Command Line Setup

1. Open a terminal with administrative privileges (e.g., Command Prompt or PowerShell).
2. Navigate to the runner's directory:

   ```cmd
   cd C:\actions-runner
   ```

3. Configure the runner using the token from Step 1:

   ```cmd
   .\config.cmd --url <your-repo-or-org-url> --token <your-token>
   ```

4. Follow the prompts to complete the configuration.

## Step 3: Install and Start the Runner as a Service

### Installing the Service

1. From the runner directory, install the runner as a Windows service:

   ```cmd
   .\svc.cmd install
   ```

### Starting the Service

2. Start the service:

   ```cmd
   .\svc.cmd start
   ```

3. Verify the service is running by checking the **Services** panel in Windows or by observing the terminal output.

## Step 4: Verify the Runner in GitHub

1. Return to the **Actions** > **Runners** settings page on GitHub.
2. Verify that your runner appears as "Online".

## Step 5: Use Your Runner in Workflows

Update your GitHub Actions workflow to use your self-hosted runner. For example:

```yaml
name: CI

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: self-hosted
    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Run a script
        run: echo "Hello from self-hosted runner!"
```
example for dotnet core, reactjs  vite https://github.com/chitmeo/chitmeo/blob/develop/.github/workflows/dotnet-desktop.yml
## Maintenance Tips

- **Update the Runner:** Periodically check for updates and download the latest runner version from GitHub.
- **Monitor Performance:** Ensure the runner has sufficient resources and is not overloaded with tasks.
- **Secure Your Machine:** Keep your Windows OS and software up to date to avoid security vulnerabilities.

---
