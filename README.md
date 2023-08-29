# Contribution Guidelines

These guidelines instruct how to submit issues and contribute to code for website.

- [Code contributions](#code-contributions)
- [Branching](#branching)
  - [Branch naming](#branch-naming)
- [Commits](#commits)
  - [Commit Message Format](#commit-message-format)
    - [Commits on the `main` branch](#commits-on-the-main-branch)
    - [Commits on other branches](#commits-on-other-branches)
  - [Conventional Commits specification](#conventional-commits-specification)
    - [Commit Message Header](#commit-message-header)
      - [Type](#type)
      - [Scope](#scope)
      - [Summary](#summary)
    - [Commit Message Body](#commit-message-body)
    - [Commit Message Footer](#commit-message-footer)
- [Pre-commit checks](#pre-commit-checks)
- [Pull requests](#pull-requests)
  - [PR Title](#pr-title)
  - [Content](#content)
  - [Code review](#code-review)
  - [Merging](#merging)
  - [Code checks](#code-checks)
  - [Security](#security)

## Code contributions

If you have fixed a bug or implemented an enhancement, you can contribute
your changes via GitHub's pull requests. This is not restricted to code, on
the contrary, fixes and enhancements to documentation and tests alone are
also very valuable.

Preconditions for code contribution are having a GitHub account,
installing [Git](https://git-scm.com/) and having write access to the project.

It is suggested for each engineer to use a [GPG](https://gnupg.org/) key to sign
their commits for higher security.

## Branching

Whenever you're going to start a new piece of work, you need to create a
new branch from the `main` one. To do so, please follow these steps:

- make sure that you are synchronized with the `main` branch by executing `git pull`
- create new branch with `git branch ticket_number-username/branch-name` or create and
  checkout to it with `git checkout -b ticket_number-username/branch-name`

### Branch naming

To keep the repository clean, everyone needs to adhere to the following
rules of branch naming:

- branch name must start with the Jira ticket number
- the Jira ticket number must be followed with a username of its creator
- the second part is a title of the branch that shortly explains what it
  contains
- username and title must be separated with a slash (`/`)
- the title must stay short but descriptive
- split names in title using hyphen (`-`)

**Good** examples: `add-118-mnojek/add-contribution-guide`, `add-118-rkuc/fix-maven-repos-likes-count`

**Bad** examples: `data-branch`, `rkuc/bugfix1`

## Commits

Commit message is a short description of the work done in a single commit.
It's important to keep the style of the commit messages consistent across
the whole repository, especially when the repository is public or the
messages are used for automation (e.g. generation of release notes).

A commit message should reflect the content of the commit.

Commit messages on a branch under the review are mostly used for the
development purposes and will not be a part of the `main` branch history.
It's up to the developer how they are going to be named, but it's
recommended to use the same rules consistently. The most important one is
the commit message related to the merged commit.

### Commit Message Format

It's important to differentiate between commits on the `main` branch, and all other
commits done on other branches.

#### Commits on the `main` branch

Our `main` branch history is used to generate release notes and it must comply with the
[Conventional Commits specification](https://www.conventionalcommits.org).

> It is very important to always make sure, that the PR being merged to the `main` branch,
> follows the convention.

Commits will be validated against the convention during PR creation (or any operation
around the PR), and those that do not comply will fail the check, making it impossible
to merge the PR.

#### Commits on other branches

Commits on other branches can be created in any way, but it is recommended to follow the
Conventional Commits approach here as well, just as a training to learn the rules.

These commits are always going to be squashed into one, so the information from
every commit will be lost. Make sure to always give a meaningful message of the squashed
commit based on the whole scope of the PR (see rules below).

### Conventional Commits specification

Full documentation is available [here](https://www.conventionalcommits.org), but some
main rules are described below.

Each commit message contains a **header**, a **body** and a **footer**:

```text
<header>
<BLANK LINE>
<body>
<BLANK LINE>
<footer>
```

The header is mandatory and must conform to the
[Commit Message Header](#commit-message-header) format.

The body is optional, but highly recommended. When the body is present it must conform
to the [Commit Message Body](#commit-message-body) format.

The footer is optional.
The [Commit Message Footer](#commit-message-footer) format describes what the footer
is used for and the structure it must have.

#### Commit Message Header

```text
<type>(<scope>): <short summary>
  │       │             │
  │       │             └─⫸ Summary in present tense. Not capitalized. No period at the end.
  │       │
  │       └─⫸ Commit Scope: website|*
  │
  └─⫸ Commit Type: build|ci|docs|feat|fix|perf|refactor|revert|style|test
```

The `<type>` and `<summary>` fields are mandatory, the `(<scope>)` field is optional.

##### Type

The type specifies the character of the changes from the commit.

Must be one of the following:

- **build**: Changes that affect the build system or external dependencies
- **ci**: Changes to our CI configuration files and scripts (examples: GitHub, docker)
- **docs**: Documentation only changes
- **feat**: A new feature
- **fix**: A bug fix
- **perf**: A code change that improves performance
- **refactor**: A code change that neither fixes a bug nor adds a feature
- **revert**: Any operation that reverts the previous commit followed by the header of the
  reverted commit
- **style**: Linting changes like: indentation, trailing commas, semi-colons
- **test**: Adding missing tests or correcting existing tests

Most important types are **feat** and **fix** because they are marking the commits that
contain production changes affecting our users. These commits will be a part of the
generated release notes.

##### Scope

The scope specifies the area which is affected by the commit.

The following is the list of supported scopes:

- website
- `*`(anything else that follows a [kebab-case](https://en.wikipedia.org/wiki/Letter_case#Kebab_case))

##### Summary

A brief but meaningful description of the change.
Here are recommendations for writing your subject:

- use the imperative, present tense: "change" (not "changed" or "changes")
- don't capitalize the first letter
- no "." (dot) at the end

#### Commit Message Body

Explain the motivation for the change in the commit message body.
This commit message should explain why you are making the change.
You can include a comparison of the previous behavior with the new behavior in order to
illustrate the impact of the change.

If your commit contains any UI-related changes, a video or screenshots should be added to the PR

#### Commit Message Footer

The footer can contain information about breaking changes and deprecations and is also
the place to reference GitHub issues, and other PRs that this commit is related to.

## Pre-commit checks

Before a commit is created, but after it is triggered from command line,
pre-commit checks are being run. Their role is to make sure that the code is
ready being committed, i.e. it meets code quality standards. It runs only
for the parts of the code that were modified and rejects the commit if any
check fails.

To install pre-commit tool, you need to have Python installed and run:

```shell
pip install pre-commit
```

After that, install the pre-commit scripts for the repository by running:

```shell
pre-commit install
```

Now, all commits that you initiate will trigger pre-commit checks and test
your code against the rules defined in the `.pre-commit-config.yaml` file.

## Pull requests

GitHub pull requests (PRs) are the main mechanism to contribute code. When you
want your work to be submitted to the `main` branch, you need to push your
changes to `remote` and create a pull request.

If you go to [Pull requests](https://github.com/Archipelo/top/pulls) tab in
GitHub project after you pushed your changes, you should see a notification
about your branch waiting to be created as pull request. Otherwise, you can
click on "New pull request" button.

### PR Title

A PR title must comply with the [commit message header](#commit-message-header) rules.
PRs with invalid titles will be marked with "Invalid PR title" label.

### Content

We are using a
[PR template](https://github.com/Archipelo/website/blob/main/.github/pull_request_template.md)
to align with the [Conventional Commits specification](#conventional-commits-specification).

> It's recommended to create PRs that have one purpose, otherwise it will be very difficult
> to define the [type](#type) and [scope](#scope) for the changes.

The PR title is the commit message header, while the PR description serves as a commit
body and commit footer.

Consider adding a **description** with a list of main changes introduced by your
pull request. This will help the reviewers quickly assess the content of the
PR without the need of reading individual commits.

Feel free to also add **labels** to allow for simple and fast search of PRs
related to a specific area.

> Avoid creating big PRs - they unnecessarily hinder the code review process
> and make the PR more liable to errors.

### Code review

Each pull request needs to be **approved by at least 1 reviewer** upon merging.

**If you're a reviewer:**

- try to provide a review as soon as it was requested from you,
- focus on the code being changed, but also think about the context,
- use "Request changes" feature when you feel some change is required,
- notify the author if UI changes were not proven by related screenshots or a video,
- comment when you have concerns or questions without a specific solution,
- check your previous comments and resolve them to unblock the PR from being
  merged,
- be polite - review the code, not the coder.

**If your work is being reviewed:**

- address all incoming comments and questions
- preferably, let the comment's author resolve the conversation (he's the one
  who had concerns),
- don't hesitate to update code if changes are requested,
- ping people when the PR is not being reviewed for a long time,
- check status of automatic checks and resolve or raise issues when a
  problem was found.

### Merging

Currently, the only possible strategy of merging a pull request is **"Squash
and merge"**. That means, that all pull request's commits will be squashed
into a single commit and merged to the base (usually `main`) branch.
This strategy helps to keep a clean history on the `main` branch. No matter
how many commits you create on your working branch, the merged work will be
reflected by one commit.

> By default, the squashed merge commit will use the PR title as its header,
> and the PR description as its body and footer.

Merge is enabled only if:

- all conversations were resolved,
- there is at least 1 approval from the reviewers,
- (if any changes were requested) a re-review from the person requesting
  changes is done,
- all required checks executed with a success state,
- the branch is up-to-date with the base branch,
- the PR title comply with [convention](#conventional-commits-specification).

### Code checks

Code checks are being executed using GitHub Actions, and they are defined in
`.github` directory.
Depending on the content of the PR, there will be some automatic build
checks triggered when the PR is created. Their purpose is to verify if the
proposed changes are:

- compliant with our coding guidelines,
- working correctly without errors,
- do not decrease the code coverage,
- passing against related test suites.

Some checks are marked as required, and they will block the PR from merging
if they fail.

### Security

We have a Dependabot feature enabled for the repository which scans our
codebase for possible vulnerabilities. List of found security alerts can be
found [here](https://github.com/Archipelo/top/security/dependabot) (not
everyone has access to it - for more info reach out to @dom). Also, Dependabot
occasionally creates PRs with updated versions of dependencies to mitigate
the risk of using outdated packages.
