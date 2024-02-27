---
title: "Git rebase"
datePublished: Wed May 31 2023 11:32:05 GMT+0000 (Coordinated Universal Time)
cuid: clibmnya9000209lbgxglfy1s
slug: git-rebase

---

Git rebase is commonly used in the following scenarios:

1. When integrating changes from one branch to another: If you have a feature branch that has diverged from the main branch (e.g., "master") and you want to incorporate the latest changes from the main branch into your feature branch, you can use git rebase.
    

Example:

```markdown
$ git checkout feature-branch
$ git rebase master
```

This will apply the commits from the "master" branch on top of the "feature-branch", resulting in a linear commit history.

1. When cleaning up commit history: If you have made several small and frequent commits in your branch, and you want to clean up the commit history before merging the branch, you can use git rebase to combine or squash multiple commits into fewer, more meaningful commits.
    

Example:

```markdown
$ git rebase -i HEAD~3
```

This will open an interactive rebase window, allowing you to pick, squash, edit, or drop commits. By combining or squashing commits, you can create a cleaner commit history.

1. When resolving conflicts during a merge: If conflicts occur while merging changes from one branch into another, using git rebase can provide a more granular and interactive conflict resolution process.
    

Example:

```markdown
$ git checkout feature-branch
$ git rebase master
```

During the rebase process, if conflicts arise, you can resolve them commit by commit, ensuring a cleaner merge process.

1. When maintaining a linear commit history: Some teams prefer to have a linear commit history, especially for long-running branches or feature branches with multiple collaborators. Git rebase allows you to keep a more straightforward and linear commit history instead of having a complex merge commit-graph.
    

Example:

```markdown
$ git checkout feature-branch
$ git rebase master
```

By rebasing your branch on top of the target branch (e.g., "master"), you can keep a clean and linear commit history.

It's important to note that using git rebase can rewrite commit history, so it should be used with caution, especially in shared or public repositories. Communication and collaboration with the team are essential to ensure everyone is aware of the changes and potential conflicts that may arise.

## Rebasing onto a commit

Rebasing a branch onto a specific commit in Git is aimed at achieving a cleaner, more linear history and integrating changes from one part of a project into another in a seamless manner. Let's delve into a practical example to illustrate the concept and its benefits more clearly.

### Scenario

Imagine you're working on a new feature for a project in a branch called `feature-x`. The project's main branch is called `main`. While you've been working on `feature-x`, several important updates and bug fixes have been made to the `main` branch. To ensure that `feature-x` incorporates these updates and is based on the latest version of `main`, you decide to rebase `feature-x` onto the latest commit of the `main` branch.

### Initial State

* **Main Branch (**`main`): A-B-C-D
    
* **Feature Branch (**`feature-x`): A-B-E-F
    

Here, `A` and `B` represent initial commits that are common to both branches. Commits `C` and `D` were made to `main` after the `feature-x` branch was created, and `E` and `F` are commits unique to `feature-x`.

### Objective

You want to update `feature-x` so it includes the changes from `C` and `D`, and still retains its unique changes (`E` and `F`), but starts from commit `D`.

### Steps to Achieve This

1. **Identify the Latest Commit on** `main`: This is commit `D` in our example.
    
2. **Rebase** `feature-x` onto Commit `D`:
    

Before rebasing, the branches look like this:

```python
main:       A - B - C - D
             \
feature-x:    E - F
```

After rebasing, you want them to look like this:

```python
main:       A - B - C - D
                         \
feature-x:                E' - F'
```

3. **Execute the Rebase**:
    
    * Check out to `feature-x` and start the rebase:
        
        ```bash
        git checkout feature-x
        git rebase main
        ```
        
    
    This moves the base of `feature-x` from `B` to `D`, and reapplies commits `E` and `F` on top of `D`, resulting in new commits `E'` and `F'` (they are new because their parent has changed, hence their content and commit hashes might also change if there were any conflicts resolved during the rebasing process).
    

### What We Achieve

* **Linear History**: The `feature-x` branch now appears as if it was created from the latest commit on `main`, making the project history easier to understand.
    
* **Incorporated Updates**: `feature-x` now includes all the updates and bug fixes (`C` and `D`) that were made to `main` after `feature-x` was originally branched off.
    
* **Easier Integration**: Merging `feature-x` back into `main` will be straightforward because it's based on the latest commit of `main`. This reduces the likelihood of merge conflicts.
    

### Conclusion

Rebasing onto a specific commit, especially in a feature branch scenario, helps ensure that your work is built on the most up-to-date base. This practice facilitates easier merges, keeps the project history cleaner, and helps avoid the complexities associated with divergent project histories.