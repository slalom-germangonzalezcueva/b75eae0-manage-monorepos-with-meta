# b75eae0-manage-monorepos-with-meta
Mange monorepos example TypeScript for Meta + AI Training (hash b75eae0)

## Pre-requisits

- `brew` command (for mac users) to easy mange packages.
- `npm` command to install dependencies.
- `gh` command to easy create pull requests.

## Instructions

1. Create and clone the meta repo (motherhsip)
2. Install the meta globally `npm i -g meta`
3. If your `motership` repo does not have the .meta or has not being initilized run `meta init`


```zsh
# Install dependencies
brew install node
brew install gh

# Login into Github (use HTTPS)
gh auth login

# Create folder sturcuter
mkdir ~/example/
cd ~/example/

# Clone the repo
gh repo clone slalom-germangonzalezcueva/b75eae0-manage-monorepos-with-meta

# Initialize meta
cd b75eae0-manage-monorepos-with-meta/
meta init

# Import existing repos and add them to the .gitignore to aovid nesting
meta project import b75eae0-repo1 https://github.com/slalom-germangonzalezcueva/b75eae0-repo1.git
echo "b75eae0-repo1/**" >> .gitignore

meta project import b75eae0-repo2 https://github.com/slalom-germangonzalezcueva/b75eae0-repo2.git
echo "b75eae0-repo2/**" >> .gitignore
```

## Use cases

### 1. Creating a version change

> Note: We will use Cursor as AI.

First checkout main and pull the resent code.

```zsh
meta git checkout main
meta git pull
```

Create a new branch for all the repos

```zsh
meta git checkout -b chore/change-package-versions 
```

Review that all repos are in the same branch.

```zsh
meta git status
```

Open this project with cursor and in the new Chat agent add context the base project and prompt:

```text
Check all the projects listed in the `.meta` file and update the `version` to `2.0.0` on `package.json` of each project. Only go 1 depth long no need to search for all the files.
```