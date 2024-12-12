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

# Hosting your own runners
