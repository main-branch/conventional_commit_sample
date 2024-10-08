# Minimal Setup for Enforcing Conventional Commits

[![Conventional
Commits](https://img.shields.io/badge/Conventional%20Commits-1.0.0-%23FE5196?logo=conventionalcommits&logoColor=white)](https://conventionalcommits.org)

This repository serves as an example for how to setup and enforce conventional
commits. See [Conventional Commits
1.0.0](https://www.conventionalcommits.org/en/v1.0.0/) for more information.

* [Why Conventional Commits?](#why-conventional-commits)
* [Implementation Details](#implementation-details)
* [Getting Started](#getting-started)
  * [Prerequisites](#prerequisites)
  * [Step-by-step](#step-by-step)

## Why Conventional Commits?

Conventional Commits provide a standardized format for commit messages that helps
automate and streamline development workflows. Adopting this practice benefits your
project in several ways:

* **Improve Readability**

   A consistent message structure makes commits easier to
   read and understand.

* **Automated Changelog Generation**

   Commit messages can be parsed to automatically
   generate a changelog, useful for continuous integration and release automation.

* **Semantic Versioning Integration**

   The commit structure supports semantic
   versioning by including types like feat and fix, which correspond to version
   updates.

* **Enforces Good Practices**

   Encourages thoughtful and informative commit
   messages, improving collaboration and making it easier to track changes over time.

By using Conventional Commits, your team can improve consistency, maintainability,
and automation in version control processes.

## Implementation Details

Conventional Commits are enforced at two levels in this setup:

1. **Pre-commit Hook**:

   A Git commit-msg hook ensures every commit message follows
   the correct format *before* it is finalized. This prevents incorrectly formatted
   commits from being made.

2. **GitHub Action**

   A GitHub Action checks that all commits in a pull request
   adhere to Conventional Commits guidelines, ensuring consistent commit messages
   across the project.

## Getting Started

### Prerequisites

Ensure that Node.js is installed and available from the command line.

### Step-by-step

1. Copy the following files into your project structure:

   ```text
   <project root>
   ├── .commitlintrc.yml
   ├── .github
   │   └── workflows
   │       └── enforce_conventional_commits.yml
   ├── .gitignore
   ├── .husky
   │   └── commit-msg
   └── package.json
   ```

   If your project already has one of these example files (such as `.gitignore`
   or `pacakge.json`), make sure to *merge* the contents of the example file into
   your existing file.

2. Modify `.commitlintrc.yml` as needed for your project. For example, you might want
   to customize the allowed commit types, scopes, or disable scopes altogether. See
   [commitlint rules](https://commitlint.js.org/reference/rules.html) for more
   information.

3. To enable the Git hook, run the following command (with Node.js installed) *after*
   all the files are put into place:

   ```shell
   npm install
   ```

   This will install the required dependencies and enable the commit-msg hook.
