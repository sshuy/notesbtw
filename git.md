# Git Tips and Tricks

## Searching through a log.
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

- [Compresses and packs](https://git-scm.com/book/en/v2/Git-Internals-Packfiles)files to stoer them more effciently.
- Removes duplicate files that are the same across multiple commits. EG: if a file remains the same from one commit to the next. We only store that file once.
