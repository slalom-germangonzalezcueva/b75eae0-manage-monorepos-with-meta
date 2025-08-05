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

Review the edits and confirm them.

Now with meta lets commit and push the changes to the branch.

```zsh
meta git add .
meta git commit -m "feat: update package version"
# For some reason direcly git push does not work due permissiosn
meta exec 'git push --set-upstream origin chore/change-package-versions'
```

Next lets use a PR template we have in `.github/PULL_REQUEST_TEMPLATE/pull_request_template.md` directory to ask Cursor and create a PR description for our changes and generate a command to create a Pull Request.

Open the chat and prompt:

```text
Create a `meta exec 'gh pr create ...'` command to create a PR using the template in `.github/PULL_REQUEST_TEMPLATE/pull_request_template.md` but replacing the placeholders with information done in the last changes requested.
```

Review the command and either let cursor to execute it or skip it and manually run by yourself. In this case I will let cursor to execute it.

If everything worked, then let request the PR links that where just created.

Open the chat and prompt:

```text
Can you run a `meta exec 'gh ...'` to get the PR links that where just created?
```

We let cursor to execute it and on the chat we copy the Links:

- https://github.com/slalom-germangonzalezcueva/b75eae0-repo1/pull/1
- https://github.com/slalom-germangonzalezcueva/b75eae0-repo2/pull/1

## Large case escenarios

On my current project I'm in charge of 73 repositories and I have faced the need of performing the bellow:

- Dependabot checks: We have dependabot enabled on Github, which automatically checks for new versions of packages on the repositories, it create PR automatically, but the thing is that we must ensure that new versions build and not breaks. So, meta helps to checkout the branches created by dependabot and exec `npm run build` on the repos.
- Make dependency changes: We have a project package that is used on multiple repositories, when new features are introduced, changing the code base of +20 repos can be tedious.

# Have fun!