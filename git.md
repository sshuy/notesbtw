# Git Tips and Tricks

## Searching through a log
Repositories of course... can have very long logs due to a vast amount of commits to the project during its lifecycle. All commits represent the *full state* of the repository at a given point in time.

We can use the <ins>git log</ins> command to see the history of commits in a repo. This command shows
- Who made the commit.
- When the commit was made.
- What was changed in the repo.

Each commit will have a unique identifier, which is called a *commit hash*. A commit hash is a long string of characters normally. Below is an example.

> 5ba786fcc93e8092831c01e71444b9baa2228a4f

**HUGE TIP:** You can refer to any commit or change in Git by using the first **7** characters from the commit hash. The above example would be <ins>5ba786f</ins>

## Storing Data
Did you know that Git actually snapshots the entire list of files on a *per-commit* level! Git does not only store the changes made in that specific commit it stores the entire **snapshot**.

Even though Git stores entire snapshots, it does do some performance optimizations so that your hidden *.git* directory doesn't get to big for his **BOOTS**

- [Compresses and packs](https://git-scm.com/book/en/v2/Git-Internals-Packfiles) files to store them more effciently.
- Removes duplicate files that are the same across multiple commits. EG: if a file remains the same from one commit to the next. We only store that file once.

## Git Configuration
Important arguments/flags for **git config**
- --add    [Required flag to add a configuration value]
- --list   [Lists the currently set configuration values can add --local to this to only display local values]
- --get    [This flag paired with a key.value will return the data from that configuration value]
- --global [Sets the configuration value for your git config globally]
- --local  [Sets the configuration value for in your git config locally, which would be the local repo]
- --unset  [Removes a configuration value from the git config, can handle global and local]
- --unset-all  [Purges all instances of a key from the config]
- --remove-section [Removes an entire section from a git config]
    So lets say you have your **[core]** section that contains
    - filemode = true
    - bare = false
    - etc...
    
    and we have another section lets say hypothetical its called **[useless]** and in there we have
    - favpizza = "Pineapple"
    - bestukcountry = "Wales"

    We can remove this entire section using the *--remove-section* flag, instead of removing each key/value one-by-one.

**Examples:**
> git config --add --global user.name "awesomedude"

> git config --get user.name    [This would output 'awesomedude']

> git config --add monkey.doo "loo" [This would add monkey.doo as a configuration value, its important to note that you can add useless config values there isn't a limitation]

> git config --unset monkey.doo [Removes monkey.doo from the config]


## Git Configuration Locations
*System:* **/etc/gitconfig**, a file that configures Git for all users on the system.
*Global:* **~/.gitconfig**, a file that configurures Git for all projects assigned to specific user.
*Local:* **.git/config**, a file that configures Git for a specific project, hence the name local.
*Worktree:* **.git/config.worktree**, a file that configures Git for part of a project. 

Pretty much all of the time you'll be working with **Global** and **Local** configuration locations. It is rare to fiddle with the others. Still important to know about however.

Here is the hierarchy layout:
**The more specific/less general the location, is the config that will take priority!!**
[![Git location hierarchy](https://storage.googleapis.com/qvault-webapp-dynamic-assets/course_assets/e4S7M9u.png)
