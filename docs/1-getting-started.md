## Getting Started

Download Godot v4.5.stable.official [876b29033]

### Clone the repo

Github link [here](https://github.com/OS-Simulator-Mystery-Game/senior-design)

Using HTTPS run: 
    
    `git clone https://github.com/OS-Simulator-Mystery-Game/senior-design.git`

### Setup git hooks

Currently, these git hooks will automatically prepend your commit messages with the Jira ID number that is in your current branch name (Jira needs the Jira ID number in commits in order to track them). For example if I have a branch `OSMG-22-git-hooks`, after setting up git hooks, if I am in that branch and just write `This is a commit message` for my commit message, after I push and look at the full commit message on github it will look like `OSMG-22: This is a commit message`.

> NOTE: this command is telling git to use the .githooks directory in the `senior-design` repo rather than your current local githooks directory. If you have any existing local githooks they will no longer work.

From the main repository directory run the following command:

    `git config core.hooksPath .githooks`