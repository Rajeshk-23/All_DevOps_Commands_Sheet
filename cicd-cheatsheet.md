# CI/CD Cheatsheet

> CI/CD automates building, testing, and delivering software through repeatable pipelines.

## Table of Contents
- [GitHub Actions Workflow Syntax](#github-actions-workflow-syntax)
- [GitHub Actions Triggers](#github-actions-triggers)
- [GitHub Actions Common Actions](#github-actions-common-actions)
- [GitHub Actions Expressions & Contexts](#github-actions-expressions--contexts)
- [GitHub Actions Secrets & Matrices](#github-actions-secrets--matrices)
- [GitHub Actions CLI](#github-actions-cli)
- [GitLab CI Pipeline Syntax](#gitlab-ci-pipeline-syntax)
- [GitLab CI Pipeline Control](#gitlab-ci-pipeline-control)
- [GitLab CI Variables & Dependencies](#gitlab-ci-variables--dependencies)
- [GitLab CLI](#gitlab-cli)

## GitHub Actions Workflow Syntax

| Command / Snippet | Description |
| --- | --- |
| `name: CI` | Sets the workflow display name. |
| `on:` | Declares events that trigger the workflow. |
| `jobs:` | Defines the workflow's jobs. |
| `runs-on: ubuntu-latest` | Selects the runner for a job. |
| `steps:` | Defines ordered work within a job. |
| `uses: owner/action@v4` | Runs a versioned reusable action. |
| `run: npm test` | Runs a shell command in a step. |
| `with:` | Passes documented inputs to an action. |
| `env:` | Defines environment variables for a scope. |
| `permissions: contents: read` | Restricts the token permissions granted to a workflow. |

## GitHub Actions Triggers

| Command / Snippet | Description |
| --- | --- |
| `on: push` | Runs when commits are pushed. |
| `on: pull_request` | Runs for pull request activity. |
| `on: workflow_dispatch` | Enables manual workflow runs. |
| `on: schedule` | Runs on a POSIX cron schedule. |
| `branches: [main]` | Filters an event to the `main` branch. |
| `paths: ['src/**']` | Filters an event to changes matching paths. |

## GitHub Actions Common Actions

| Command / Snippet | Description |
| --- | --- |
| `actions/checkout@v4` | Checks out repository source code. |
| `actions/setup-node@v4` | Installs and configures Node.js. |
| `actions/setup-python@v5` | Installs and configures Python. |
| `actions/cache@v4` | Restores and saves dependency caches. |
| `actions/upload-artifact@v4` | Uploads files for later workflow use. |
| `actions/download-artifact@v4` | Downloads artifacts from the workflow. |
| `docker/login-action@v3` | Authenticates Docker to a registry. |
| `docker/build-push-action@v6` | Builds and optionally pushes Docker images. |

## GitHub Actions Expressions & Contexts

| Command / Snippet | Description |
| --- | --- |
| `${{ github.ref }}` | Evaluates to the triggering Git ref. |
| `${{ github.sha }}` | Evaluates to the triggering commit SHA. |
| `${{ github.event_name }}` | Evaluates to the event name. |
| `${{ runner.os }}` | Evaluates to the current runner operating system. |
| `${{ env.NAME }}` | Reads an environment variable from expression context. |
| `${{ vars.NAME }}` | Reads a repository or organization configuration variable. |
| `if: ${{ failure() }}` | Runs a step only after a failure. |
| `needs: [build]` | Makes a job wait for the named job. |

## GitHub Actions Secrets & Matrices

| Command / Snippet | Description |
| --- | --- |
| `${{ secrets.DEPLOY_TOKEN }}` | Reads a configured secret without printing it. |
| `strategy:` | Configures matrix or failure behavior for a job. |
| `matrix.node: [20, 22]` | Defines Node.js versions for matrix jobs. |
| `${{ matrix.node }}` | Reads the active matrix value. |
| `fail-fast: false` | Lets all matrix jobs finish after one fails. |
| `max-parallel: 2` | Limits concurrent matrix jobs. |
| `concurrency: deploy-production` | Serializes runs that share a concurrency group. |

## GitHub Actions CLI

| Command / Snippet | Description |
| --- | --- |
| `gh workflow list` | List repository workflows. |
| `gh workflow run CI --ref main` | Manually dispatch a workflow on a ref. |
| `gh run list --workflow CI` | List runs for a workflow. |
| `gh run view <run-id>` | Show a workflow run summary. |
| `gh run watch <run-id>` | Stream a run until it completes. |
| `gh run view <run-id> --log-failed` | Show logs only for failed steps. |
| `gh run rerun <run-id> --failed` | Re-run only failed jobs in a run. |

## GitLab CI Pipeline Syntax

| Command / Snippet | Description |
| --- | --- |
| `stages:` | Defines the ordered pipeline stages. |
| `build:` | Declares a job named `build`. |
| `stage: test` | Assigns a job to the `test` stage. |
| `image: node:22` | Selects the container image for a job. |
| `script:` | Defines commands the runner executes. |
| `before_script:` | Defines commands that run before every job script. |
| `after_script:` | Defines commands that run after a job script. |
| `include:` | Imports external CI configuration. |
| `default:` | Sets defaults inherited by jobs. |

## GitLab CI Pipeline Control

| Command / Snippet | Description |
| --- | --- |
| `rules:` | Selects whether and when a job is added. |
| `if: '$CI_COMMIT_BRANCH == "main"'` | Runs a rule only on the `main` branch. |
| `changes: ["src/**/*"]` | Matches a rule when listed paths changed. |
| `when: manual` | Makes a job require manual start. |
| `when: always` | Runs a job even after earlier failure. |
| `allow_failure: true` | Lets a failing job avoid failing the pipeline. |
| `only: [main]` | Limits a job to the listed refs. |
| `except: [tags]` | Excludes a job from tag pipelines. |
| `workflow: rules:` | Controls whether an entire pipeline is created. |

## GitLab CI Variables & Dependencies

| Command / Snippet | Description |
| --- | --- |
| `variables:` | Defines CI/CD variables for a scope. |
| `$CI_COMMIT_SHA` | Provides the commit SHA for the pipeline. |
| `$CI_COMMIT_REF_NAME` | Provides the branch or tag name. |
| `artifacts:` | Preserves job output for download or later jobs. |
| `paths: [dist/]` | Selects artifact files to upload. |
| `expire_in: 1 week` | Sets an artifact retention period. |
| `cache:` | Reuses files between pipeline jobs. |
| `key: $CI_COMMIT_REF_SLUG` | Uses a branch-safe cache key. |
| `needs: [build]` | Starts a job after specified jobs complete. |
| `dependencies: [build]` | Downloads artifacts from selected earlier jobs. |

## GitLab CLI

| Command / Snippet | Description |
| --- | --- |
| `glab ci list` | List recent pipelines. |
| `glab ci view <pipeline-id>` | Show a pipeline's jobs and status. |
| `glab ci trace <job-id>` | Stream the trace for a job. |
| `glab ci run` | Create a pipeline for the current ref. |
| `glab variable list` | List project CI/CD variables. |
| `glab variable set DEPLOY_ENV production` | Set a project CI/CD variable. |
