# Source Control: How I Learned to Stop Worrying, and Love Git

## Objectives

This document will provide a guide for the following topics:


- Intro to Git: Warmup Activity (15 Minutes)
- Installing Git
  - macOS
  - Windows 10
  - Linux
- Verifying Your Installation
- Generating and Configuring SSH Keys
- Cloning a Remote Repository to Your Local Machine
- Adding, Committing, and Pushing Local Changes to Remote Repositories
- [WIP] Get Advanced with Git
- More Practice/Additional Educational Resources


## Intro to Git: Warmup Activity (15 Minutes)

Before setting Git up on your development machine, consider attempting the 'Try Git' challenge!
This will allow you to get a feel for using git in a guided setting, before you run the commands on your machine. Highly recommended! [Interactive: Learn Git Online](https://try.github.io/levels/1/challenges/1)

## Installing Git

**NOTE**: $ denotes a command that must be pasted into `Terminal`/`Git Bash`.

### macOS

1. Hold down ⌘ and press the Spacebar to invoke Spotlight.
1. Type `Terminal.app`.
1. In `Terminal.app`, run the following command to install [Homebrew](https://brew.sh):

    ```bash
    /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
    ```

1. Once Homebrew is installed, run `brew install git` to install the latest version of git.

### Windows 10

1. Navigate to [Git: Download Windows Package](https://git-scm.com/download/win) in your browser.
1. If prompted, save the file.
1. Navigate to the directory you saved the file in, and double-click to install.

### Linux

#### Debian/Ubuntu:

1. Install Git via `apt` by running:

    ```bash
    sudo apt-get install git-all
    ```

#### Red Hat/CentOS:

1. Install Git via `dnf` by running:

    ```bash
    sudo apt-get install git-all
    ```

## Verifying Your Installation

1. To verify git is installed correctly, open `Terminal` (macOS/Linux) or `Git Bash` (Windows).

1. Run `git --version` within the new [shell](https://en.wikipedia.org/wiki/Shell_(computing)):
    ```bash
    $ git --version
    git version 2.15.1
    ```

## Configure Git

1. Configure your global username and email address. **IMPORTANT**: If you skip this step, Git will produce a warning each time you push to a remote branch.

    ```bash
    $ git config --global user.name "Dani Roxberry"
    $ git config --global user.email "dani@bitoriented.com"
    ```

1. Optional. Configure additional, helpful settings:

    - [**macOS/Linux**] Set the default text editor to VSCode:

        ```bash
        $ git config --global core.editor code
        ```
    - [**Windows**] On a Windows system, if you want to use a different text editor, you must specify the full path to its executable file:

        ```bash
        $ git config --global core.editor "<FULL PATH TO VSCODE EXE IN QUOTES>"
        ```

1. Double-check your settings:

    ```bash
    $ git config list

    credential.helper=osxkeychain
    user.name=Dani Roxberry
    user.email=dani@bitoriented.com
    url.ssh://git@github.com/.insteadof=https://github.com/
    mergetool.keepbackup=false
    core.excludesfile=/Users/dani/.gitignore_global
    core.editor=code
    filter.lfs.required=true
    filter.lfs.clean=git-lfs clean -- %f
    filter.lfs.smudge=git-lfs smudge -- %f
    filter.lfs.process=git-lfs filter-process
    ```
## Generating and Configuring SSH Keys

1. Run the following commands. **DO NOT ENTER A PASSWORD WHEN PROMPTED**. Just hit enter.

    ```bash
    $ ssh-keygen -t rsa -C "your.email@example.com" -b 4096
    $ cat ~/.ssh/id_rsa.pub

    ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQC+SJSGSCeSeLnOg543Hyqh3OcAENvugks8ygkoOkEA4g652gK0ES7CjjpBy4GS/XnaUWiD9iaoE4soE8dqhe/psCoiU+QxGmkjNapLtQAOu1W2v/SEh3Jao+rtfop0S+Ak96fiOVgUgupFAN1FXV1iYdpwyk7rR3Kv/T2M9Ce06Bk5KupdgNzF7Eg/tmFx8H2yVmeQ2J3MWM948ZvWmbBwtbcDRQ6ZtnXSoEof1Wg8agzyisq0Yoi3rXqAIxr1Hevs4g79Lrf65548yTfqZqyljSFA/h4VntXsZYKIWoXti5uPstrwRF6oaH8dm1l74jLAKC/XlqnsqVkRWn/Updj+x8g3+EdtFiWpUwEIMWWDbjPk0HHTfOS06716Hcji0hg4Kfipe03QjhD8Vqp/snaYCb8R3OSZOK1H3Zj9n1JgHhOoFYzk0gstV9DGRmrm2ywrQh3Q7fs23pzrZARGBhRHwk5XfFQl85D7oJffBbfpqjDdyzcHYOAo3mlDfwkfl1nHxynWrwCk+0KKD0zLVsqtkSVlNfQv2JqSSc6ox6vktO7RWKg5/T0b9r0fnNcYfGBVnoJDulJPJr7ynSUDRi2hX5WpMDomylUahVYN/VlAZBwvuWdOM0h3ZUsQEPjauN0k+mY3nQVTIa0hWl1vszTddcxLZKK5mJsvlnL7HMBQxQ== dani@bitoriented.com
    ```

1. With your mouse, highlight the entire public key, beginning with `ssh-rsa` and ending with your email address. Copy the highlighted public to the clipboard.

1. Add the key to [**GitLab**](http://ucb.bootcampcontent.com/profile/keys):
    - Click the above link and paste your key in the 'Key' section and give it a relevant 'Title'. Use an identifiable title like 'Work Laptop - Windows 7' or 'Home MacBook Pro 15'.

    - **Make sure you copied the entire key starting with `ssh-rsa` and ending with your email.**

    - Test your setup by running `ssh -T git@example.com` (replacing `example.com` with your GitLab domain) and verifying that you receive a `Welcome to GitLab` message.
        - Test using our Class Repository with this command: `ssh -T git@ucb.bootcampcontent.com`

        - You should receive the following output:

            ```bash
            $ ssh -T git@ucb.bootcampcontent.com

            Welcome to GitLab, Dani Roxberry!
            ```

1. Add the key to [**GitHub**](https://github.com/settings/ssh/new):
    - Click the above link and paste your key in the 'Key' section and give it a relevant 'Title'. Use an identifiable title like 'Work Laptop - Windows 7' or 'Home MacBook Pro 15'.

    - **Make sure you copied the entire key starting with `ssh-rsa` and ending with your email.**

    - Test your setup by running `ssh -T git@github.com`:

        ```bash
        $ ssh -T git@github.com

        Hi droxey! You've successfully authenticated, but GitHub does not provide shell access.
        ```


## Cloning a Remote Repository to Your Local Machine

```bash
$ git clone git@ucb.bootcampcontent.com:UCB-Coding-Bootcamp/UCBSAN201802DATA3-Class-Repository-DATA.git

Cloning into 'UCBSAN201802DATA3-Class-Repository-DATA'...
remote: Counting objects: 110, done.
remote: Compressing objects: 100% (96/96), done.
remote: Total 110 (delta 10), reused 0 (delta 0)
Receiving objects: 100% (110/110), 50.72 MiB | 2.69 MiB/s, done.
Resolving deltas: 100% (10/10), done.
```

## Adding, Committing, and Pushing Local Changes to Remote Repositories

```bash
$ cd ~/dev/repos/my-new-repo
$ git add .
$ git commit -m "A good, descriptive commit message."
$ git push origin master
```

## Get Advanced with Git

`COMING SOON!`

## More Practice/Additional Educational Resources

### Fundamentals

- [Getting Started: Git Overview](https://git-scm.com/book/en/v2/Getting-Started-Git-Basics)

### eBooks

- [Pro Git: Free eBook (HTML/PDF/EPUB/MOBI)](https://git-scm.com/book/en/v2)

### Videos

Quick overview of Git in video format. Each video is approximately 5 minutes long.

- [Git Basics: Episode 1 - What is Version Control? (VIDEO)](https://git-scm.com/video/what-is-version-control)
- [Git Basics: Episode 2 - What is Git? (VIDEO)](https://git-scm.com/video/what-is-git)
- [Git Basics: Episode 3 - Get Going with Git (VIDEO)](https://git-scm.com/video/get-going)
- [Git Basics: Episode 4 - Quick Wins with Git (VIDEO)](https://git-scm.com/video/quick-wins)

### GitHub

- [Cheat Sheet (PDF)](https://services.github.com/on-demand/downloads/github-git-cheat-sheet.pdf)
    - Git  is  the  open  source  distributed  version  control  system  that  facilitates  GitHub  activities  on  your  laptop  or desktop. This cheat sheet summarizes commonly used Git command line instructions for quick reference

- [GitHub Desktop](https://desktop.github.com/)
    - macOS / Windows: A desktop, GUI based Git and GitHub client.

- [VSCode: Version Control](https://code.visualstudio.com/docs/editor/versioncontrol)
    - Handy documentation for the default Source Control Manager that ships with VSCode.)

### Repositories to Note

- [git/git](https://github.com/git/git)
    - The Git source code on GitHub