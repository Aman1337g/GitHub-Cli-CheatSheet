# GitHub CLI Cheatsheet

A comprehensive guide to the most important commands in GitHub CLI (gh).

## Table of Contents
- [Installation](#installation)
- [Authentication](#authentication)
- [Core Commands](#core-commands)
- [Repository Management](#repository-management)
- [Pull Requests](#pull-requests)
- [Issues](#issues)
- [Gists](#gists)
- [GitHub Projects](#github-projects)
- [Aliases](#aliases)
- [Other Useful Commands](#other-useful-commands)

## Installation

### Ubuntu/Debian
```bash
(type -p wget >/dev/null || (sudo apt update && sudo apt-get install wget -y)) \
&& sudo mkdir -p -m 755 /etc/apt/keyrings \
&& out=$(mktemp) && wget -nv -O$out https://cli.github.com/packages/githubcli-archive-keyring.gpg \
&& cat $out | sudo tee /etc/apt/keyrings/githubcli-archive-keyring.gpg > /dev/null \
&& sudo chmod go+r /etc/apt/keyrings/githubcli-archive-keyring.gpg \
&& echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" | sudo tee /etc/apt/sources.list.d/github-cli.list > /dev/null \
&& sudo apt update \
&& sudo apt install gh -y

# If you want to use the modern DEB-822 Style Format
sudo mv /etc/apt/sources.list.d/github-cli.list /etc/apt/sources.list.d/github-cli.list.bak

sudo <your_fav_editor>(mine is nvim) /etc/apt/sources.list.d/github-cli.sources
# Put theses lines in it
Types: deb
URIs: https://cli.github.com/packages
Suites: stable
Components: main
Architectures: amd64
Signed-By: /etc/apt/keyrings/githubcli-archive-keyring.gpg
```

For other operating systems, see the [official installation guide](https://github.com/cli/cli#installation).

## Authentication

### Login to GitHub
```bash
# Interactive login
gh auth login

# Login with a specific host
gh auth login --hostname enterprise.internal

# Login using a token from a file
gh auth login --with-token < mytoken.txt
```

### Logout
```bash
# Interactive logout
gh auth logout

# Logout from a specific host and account
gh auth logout --hostname enterprise.internal --user username
```

### Check Auth Status
```bash
gh auth status
```

## Core Commands

### Browse
Open the repository in the browser
```bash
# Open current repository in browser
gh browse

# Open a specific repository
gh browse owner/repo

# Open specific issue or PR
gh browse --issue 123
```

## Repository Management

### Create Repository
```bash
# Create a new repository interactively
gh repo create

# Create a public repository
gh repo create my-project --public

# Create a repository from the current directory
gh repo create --source=. --push
```

### Clone Repository
```bash
# Clone your own repository
gh repo clone my-project

# Clone another user's repository
gh repo clone username/repo
```

### List Repositories
```bash
# List your repositories
gh repo list

# List repositories from an organization
gh repo list organization

# List repositories with specific criteria
gh repo list --private --source
```

### View Repository
```bash
# View repository details
gh repo view

# View repository details in web browser
gh repo view --web
```

### Fork Repository
```bash
# Fork a repository
gh repo fork owner/repo

# Clone the fork after forking
gh repo fork owner/repo --clone
```

## Pull Requests

### Create PR
```bash
# Create a PR interactively
gh pr create

# Create a PR with title and body
gh pr create --title "Fix bug" --body "This PR fixes a bug"

# Create a draft PR
gh pr create --draft
```

### List PRs
```bash
# List open PRs
gh pr list

# List PRs assigned to you
gh pr list --assignee @me

# List PRs with specific state
gh pr list --state closed
```

### View PR
```bash
# View PR details
gh pr view 123

# View PR in web browser
gh pr view 123 --web
```

### Checkout PR
```bash
# Checkout a PR locally
gh pr checkout 123
```

### Merge PR
```bash
# Merge a PR
gh pr merge 123

# Merge with specific strategy
gh pr merge 123 --squash
```

## Issues

### Create Issue
```bash
# Create an issue interactively
gh issue create

# Create an issue with title and body
gh issue create --title "Bug report" --body "There is a bug"

# Create an issue with labels and assignees
gh issue create --label bug,urgent --assignee username
```

### List Issues
```bash
# List open issues
gh issue list

# List issues assigned to you
gh issue list --assignee @me

# List issues with specific label
gh issue list --label bug
```

### View Issue
```bash
# View issue details
gh issue view 123

# View issue in web browser
gh issue view 123 --web
```

## Gists

### Create Gist
```bash
# Create a gist from file
gh gist create file.txt

# Create a private gist
gh gist create file.txt --private

# Create a gist with description
gh gist create file.txt --desc "My useful code snippet"
```

### List Gists
```bash
# List your gists
gh gist list

# List a specific user's gists
gh gist list username
```

## GitHub Projects

### List Projects
```bash
# List projects
gh project list
```

### Create Project
```bash
# Create a new project
gh project create
```

### View Project
```bash
# View project details
gh project view PROJECT_NUMBER
```

## Aliases

### Set Alias
```bash
# Create a simple alias
gh alias set pv 'pr view'

# Create an alias with placeholders
gh alias set epicsBy 'issue list --author="$1" --label="epic"'

# Create a shell alias
gh alias set --shell igrep 'gh issue list --label="$1" | grep "$2"'
```

### List Aliases
```bash
gh alias list
```

### Delete Alias
```bash
# Delete a specific alias
gh alias delete alias-name

# Delete all aliases
gh alias delete --all
```

## Other Useful Commands

### API Requests
```bash
# Make a GET request
gh api repos/owner/repo

# Make a POST request with data
gh api repos/owner/repo/issues -f title="Bug" -f body="Description"
```

### Workflow Management
```bash
# List workflows
gh workflow list

# Run a workflow
gh workflow run workflow.yml

# View a workflow
gh workflow view workflow.yml
```

### Secrets Management
```bash
# Set a secret
gh secret set SECRET_NAME

# List secrets
gh secret list
```

## Need Help?

For detailed information on any command, use:

```bash
gh help [command]
```

For full documentation, visit the [GitHub CLI documentation](https://cli.github.com/manual/).
