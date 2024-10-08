# Minimal Setup for Enforcing Conventional Commits

[![Conventional
Commits](https://img.shields.io/badge/Conventional%20Commits-1.0.0-%23FE5196?logo=conventionalcommits&logoColor=white)](https://conventionalcommits.org)

This repository provides a minimal setup for enforcing Conventional Commits in your
project. By following the steps outlined here, you can ensure that all commits in
your repository adhere to a standardized format, which helps streamline collaboration
and automate release workflows.

The key objectives of this setup are:

1. Developers must use Conventional Commits when making commits to pull requests.
2. All commits merged into a release branch must follow the Conventional Commit
   standard.

For more information, refer to the [Conventional Commits 1.0.0
specification](https://www.conventionalcommits.org/en/v1.0.0/).

* [Why Conventional Commits?](#why-conventional-commits)
* [Implementation Details](#implementation-details)
* [Getting Started](#getting-started)
  * [1. Add conventional commit enforcement to your project](#1-add-conventional-commit-enforcement-to-your-project)
  * [2. Modify `.commitlintrc.yml` as Needed for Your Project](#2-modify-commitlintrcyml-as-needed-for-your-project)
  * [3. Enable the `commit-msg` Git hook](#3-enable-the-commit-msg-git-hook)
  * [4. Define Branch and Merge Rules in GitHub](#4-define-branch-and-merge-rules-in-github)
* [The Case Against Conventional Commits](#the-case-against-conventional-commits)

## Why Conventional Commits?

Conventional Commits provide a standardized format for commit messages that helps
automate and streamline development workflows. Adopting this practice benefits your
project in several ways:

* **Improve Readability**

   A consistent message structure makes commits easier to read and understand.

* **Automated Changelog Generation**

   Commit messages can be parsed to automatically generate a changelog, useful for
   continuous integration and release automation.

* **Semantic Versioning Integration**

   The commit structure supports semantic versioning by including types like feat and
   fix, which correspond to version updates.

* **Enforces Good Practices**

   Encourages thoughtful and informative commit messages, improving collaboration and
   making it easier to track changes over time.

By using Conventional Commits, your team can improve consistency, maintainability,
and automation in version control processes.

## Implementation Details

Conventional Commits are enforced at two levels in this setup:

* **Pre-commit Hook**:

   A Git commit-msg hook ensures every commit message follows the correct format
   *before* it is finalized. This prevents incorrectly formatted commits from being
   made.

* **GitHub Action**

   A GitHub Action checks that all commits in a pull request adhere to Conventional
   Commits guidelines, ensuring consistent commit messages across the project.

## Getting Started

Ensure that Node.js is installed and available from the command line.

### 1. Add conventional commit enforcement to your project

   Copy the following files into your project structure:

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

   If your project already has one of these example files (such as `.gitignore` or
   `package.json`), make sure to *merge* the contents of the example file into your
   existing file.

### 2. Modify `.commitlintrc.yml` as Needed for Your Project

   You might want to customize the allowed commit types, scopes, or disable scopes
   altogether. See [commitlint rules](https://commitlint.js.org/reference/rules.html)
   for more information.

### 3. Enable the `commit-msg` Git hook

   Run the following command (with Node.js installed) *after* all the files are put
   into place:

   ```shell
   npm install
   ```

   This will install the required dependencies and enable the commit-msg hook.

### 4. Define Branch and Merge Rules in GitHub

To enforce Conventional Commits and maintain a clean commit history, update the
following GitHub settings for your repository.

* **Disallow merge commits and squash merges**

  Only allow rebase merges to ensure all commits merged into the main branch follow
  the Conventional Commits format.

  Navigate to **Settings > General** in your GitHub repository. In the "**Pull
  Requests**" section:

  * Uncheck "**Allow merge commits**"
  * Uncheck "**Allow squash merging**"
  * Check "**Allow rebase merging**"

* **Enforce commit linting checks**

  Require all pull requests to pass the commit linting check before merging.

  Navigate to **Settings > Rules > Rulesets** and select (or create) the ruleset that
  applies to the main branch.

  * Check “**Require a pull request before merging**” and enable all related options
  * Check "**Require status checks to pass**" and add the status check for "**Verify
    Convention Commits**" (or refer to the exact name of your commit linting check as
    defined in your workflow file)

* **Require a linear history**

  Enforce a linear history to maintain a straightforward and uncluttered commit log.

  Navigate to **Settings > Rules > Rulesets** and select (or create) the ruleset that
  applies to the main branch.

  * Check "**Require linear history**"

## The Case Against Conventional Commits

While **Conventional Commits** are widely adopted for their structure and clarity,
there are some criticisms associated with their use.

* **Increased Burden on Developers**

   **Learning Curve**: For teams unfamiliar with the Conventional Commits
   specification, there’s a learning curve. Developers must understand and
   consistently apply the commit message structure (e.g., using types like `feat`,
   `fix`, `chore`).

   **Time-Consuming**: Writing precise, well-structured commit messages can be
   time-consuming, especially when developers are focused on solving technical
   problems and might consider the format as a distraction.

* **Potential for Overhead in Small Teams**

   **Overkill for Simple Projects**: In smaller projects or teams, adhering strictly
   to Conventional Commits may feel unnecessary or overly formal. Some developers
   argue that this level of structure isn’t needed unless the project is very large
   or has many contributors.

   **Non-Trivial Tooling**: Implementing Conventional Commits often requires
   additional tooling (e.g., commit linting, changelog generation). This can add
   complexity to the CI/CD pipeline, which may not be justified for small-scale or
   personal projects.

* **Reduced Flexibility**

   **Rigid Structure**: The predefined types (`feat`, `fix`, etc.) may not cover all
   possible use cases or workflows. This rigidity can feel limiting to developers who
   are used to a more freeform approach to writing commit messages.

   **Imprecise Classifications**: Sometimes, developers struggle to classify their
   commits accurately. For example, determining whether a commit should be a `fix`,
   `refactor`, or `chore` can be subjective and inconsistent across a team.

* **Focus on Syntax over Meaning**

   **Syntax Over Substance**: Critics argue that developers might prioritize adhering
   to the correct commit format rather than focusing on writing a meaningful commit
   message. This can lead to superficial messages that follow the rules but lack
   clarity or detail.

   **Superficial Changelogs**: While changelogs generated from conventional commits
   are structured, they might not provide sufficient detail for users. A changelog
   full of `feat: added X` and `fix: resolved Y` entries might lack meaningful
   explanations or context.

* **Enforcing Conventional Commits Can Be Disruptive**

   **Hinders Development Flow**: Developers who are used to committing frequently and
   quickly, especially in fast-paced environments, may find the process of crafting
   well-structured commit messages disruptive to their workflow.

   **Merge Commit Challenges**: In some workflows, particularly when using pull
   requests or merge commits, it can be difficult to maintain consistency with
   Conventional Commits. Developers may need to reword or squash commits to ensure
   they follow the required format, adding extra steps to the workflow.

* **Not Always a Perfect Fit for Non-SemVer Projects**

   **SemVer Dependency**: Conventional Commits are closely tied to Semantic
   Versioning (SemVer). Projects that don’t follow SemVer (e.g., libraries or
   services with continuous deployment) may find the specification less useful or
   irrelevant, making the overhead less justified.

* **Discourages Granular Commits**

   **Encourages Batching Changes**: To avoid creating too many “small” commit
   messages, some developers may batch unrelated changes into a single commit to
   simplify the commit process. This goes against the best practice of making
   granular, single-purpose commits.

* **Limited Adaptation for Non-Code Changes**

   **Non-Code Commit Ambiguity**: For non-code contributions, such as documentation
   or configuration changes, the commit types can feel awkward. While types like
   `docs` or `chore` exist, they might not fully capture the intention or scope of
   such changes, leading to confusion.
