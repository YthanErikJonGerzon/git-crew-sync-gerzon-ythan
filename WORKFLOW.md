# Git Crew Sync Workflow

## Task 1 — Push a Change from Clone A

In Clone A, I checked out the `feature/overtime-pay` branch and added overtime pay for shifts over 8 hours. The overtime hours are paid at 1.5 times the regular hourly rate. I tested the change and successfully committed and pushed it to the shared GitHub repository.

### Task 1 Evidence

![Task 1 Evidence](screenshots/task1.png)


## Task 2 — Diverge from Clone B and Get Rejected

In Clone B, I made a different change to the same `calculatePay()` function by changing the calculation from truncating the result with `Math.floor()` to rounding it with `Math.round()`.

When I tried to push the change, Git rejected the push because the remote branch already contained a commit from Clone A that Clone B did not have. The error said that the tip of my current branch was behind its remote counterpart and that I needed to integrate the remote changes before pushing.

### Task 2 Evidence

![Task 2 Evidence](screenshots/task2.png)


## Task 3 — Reconcile with a Merge

In Clone B, I first fetched the latest changes from the remote repository and then merged `origin/feature/overtime-pay`. Git detected a conflict in `shifts.js` because both changes modified the `calculatePay()` function.

I manually resolved the conflict so that both behaviors were preserved. The calculation supports overtime pay and the rounding behavior. I then ran the tests and all tests passed. After resolving the conflict, I created a merge commit and successfully pushed the merged branch to GitHub.

### Task 3 Evidence

![Task 3 Evidence](screenshots/task3.png)


## Task 4 — Reconcile with a Rebase

In Clone A, I made another change to the `calculatePay()` function without fetching the latest remote changes first. When I tried to push, Git rejected the push because the remote branch contained commits that Clone A did not have.

I then fetched the latest changes and used `git rebase origin/feature/overtime-pay`. Git detected a conflict in `shifts.js`. I manually resolved the conflict, ran the tests, and all tests passed. I then continued the rebase successfully.

The main difference between the merge in Task 3 and the rebase in Task 4 is that the merge combined the two histories and created a merge commit. The rebase replayed the local work on top of the updated remote history, producing a more linear history.

### Task 4 Evidence

![Task 4 Evidence](screenshots/task4.png)


## Task 5 — Merge into Main

After completing the `feature/overtime-pay` branch, I switched to the `main` branch and merged the finished feature branch into it. I ran the tests and then pushed the updated `main` branch to the GitHub repository.

### Task 5 Evidence

![Task 5 Evidence](screenshots/task5.png)


## Task 6 — Tag the Final Commit

I created the `v1.0-synced` tag on the final commit and pushed the tag to GitHub using `git push --tags`. The tag was successfully created and pushed to the remote repository.

### Task 6 Evidence

![Task 6 Evidence](screenshots/task6.png)


# Written Answers

## 1. What did the rejected push error message tell you, and why did it happen?

The rejected push message told me that my local branch was behind the remote branch and that Git could not perform a fast-forward update. It happened because another clone had already pushed changes to the same remote branch. My local repository did not have those changes yet, so Git rejected my push to prevent the remote changes from being overwritten.


## 2. What's the actual difference between how you resolved Task 3 (merge) vs Task 4 (rebase)?

In Task 3, I used a merge to combine the changes from the remote branch with the changes in Clone B. Git created a merge commit that connected both histories.

In Task 4, I used a rebase instead. I fetched the latest remote changes and replayed my local commit on top of the updated remote branch. This resulted in a more linear history instead of creating another merge commit.


## 3. What one habit would have avoided both rejected pushes in this lab?

One habit that would have avoided both rejected pushes is checking for and fetching the latest remote changes before starting work or pushing. Keeping the local branch synchronized with the shared remote makes it less likely that another teammate's changes will cause a non-fast-forward rejection.


## 4. Which approach — merge or rebase — would you default to on a shared team branch, and why?

I would default to merge on a shared team branch because it preserves the actual history of the team's work and does not rewrite commits that other developers may already have. Rebase is useful for keeping a private local branch organized, but merging is safer when working directly on a branch shared by multiple developers.