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