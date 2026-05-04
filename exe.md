Git & GitHub Practice Session
Overview
This session takes participants from zero to a working pull-request workflow in two hours. The first hour focuses on local Git mechanics — making commits, branching, and merging on their own machine. The second hour moves to GitHub, where they push their work, open a pull request, review a teammate's code, and merge it in.
Pair participants up at the start. Pairs make the GitHub portion much easier because each person needs someone to review their pull request.
Prerequisites 
    • Git configured with their name and email — see commands below

git config --global user.name "Their Name"
git config --global user.email "their.email@example.com"
git config --global init.defaultBranch main
Part 1 — Local Git (45 minutes)
Goal: by the end of this part, every participant has a local repository with several commits across two branches, and has merged one branch into another.
Exercise 1.1 — Create a repo and make your first commits (15 min)
    1. Create a new folder on the desktop called recipe-book and move into it.
mkdir recipe-book
cd recipe-book
    2. Initialize Git in this folder.
git init
    3. Create a file called README.md with a one-line description of the project. Use any editor.
    4. Check what Git sees.
git status
Discuss what "untracked" means — Git can see the file but isn't watching it yet.
    5. Stage the file, then commit it.
git add README.md
git commit -m "Add README"
    6. Add a second file called pancakes.md with a pancake recipe. Stage and commit it separately.
    7. Add a third commit that edits pancakes.md (change the number of eggs, for instance). Then look at the history.
git log --oneline

Checkpoint — everyone should see three commits in their log before moving on.

Exercise 1.2 — Branching and merging (20 min)
    8. Create a branch called add-waffles and switch to it.
git switch -c add-waffles
    9. On this branch, create waffles.md with a waffle recipe. Commit it.
    10. Switch back to main and confirm waffles.md is no longer there.
git switch main
ls.
    11. Merge the branch back into main.
git merge add-waffles
    12. Delete the merged branch.
git branch -d add-waffles
Exercise 1.3 — Create a merge conflict on purpose (10 min)
Conflicts feel scary the first time. Manufacturing one in a safe setting removes the fear.

    13. Create two branches from main: edit-a and edit-b.
    14. On edit-a, change the first line of pancakes.md to something. Commit.
    15. Switch to edit-b, change the same first line to something different. Commit.
    16. Switch to main, merge edit-a (clean), then try to merge edit-b.
git merge edit-b
    17. Notice the  <<<<<<< / ======= / >>>>>>> markers. Find out what they mean.
    18. Manually edit the file to the version you want, remove the markers, then:
git add pancakes.md
git commit

Note: This is what 90% of "merge conflicts" look like. Open the file, pick the right text, save, add, commit.
Break (10 minutes)
Use this time to walk around the room and unstick anyone who's behind. Everyone needs to be at the end of Part 1 before Part 2 star ts, because Part 2 builds directly on the recipe-book repo.






Part 2 — GitHub (45 minutes)
Goal: Each participant pushes their local repo to GitHub, opens a pull request against a partner's repository, reviews their partner's PR, and merges one in.
Exercise 2.1 — Push your repo to GitHub (10 min)
    19. On github.com, click the + icon in the top right and choose "New repository".
    20. Name it recipe-book. Leave it public. Do NOT initialize with a README, .gitignore, or license — the local repo already has content.
    21. On the next screen, GitHub shows commands for "…push an existing repository." Copy and run them in the terminal:
git remote add origin https://github.com/YOUR-USERNAME/recipe-book.git
git branch -M main
git push -u origin main
    22. Refresh the GitHub page. The files should be there.

Common snag: GitHub now requires a personal access token instead of a password for HTTPS pushes. If anyone gets a password prompt and gets rejected, point them to GitHub Settings → Developer settings → Personal access tokens → Tokens (classic), and have them generate one with "repo" scope.

Exercise 2.2 — Pair up and swap repos (5 min)
    23. Each person sends their partner a link to their GitHub repo.
    24. Each person clones their partner's repo into a separate folder.
cd ..
git clone https://github.com/PARTNER-USERNAME/recipe-book.git partner-recipe-book
cd partner-recipe-book

Exercise 2.3 — Open a pull request (15 min)
Now each person contributes a recipe to their partner's project.

    25. In the cloned partner repo, create a new branch.
git switch -c add-french-toast
    26. Add a french-toast.md file with a recipe. Commit it.
    27. Push the branch to GitHub.
git push -u origin add-french-toast
    28. Visit the partner's repo on GitHub. There should be a yellow banner offering to "Compare & pull request." Click it.
    29. Write a short PR title and description explaining the change. Submit the pull request.




Exercise 2.4 — Review and merge (15 min)
    30. Each person opens the pull request that was filed against their own repo.
    31. Click the "Files changed" tab. Hover over a line and click the blue + to leave a line comment. Suggest one small improvement.
    32. Submit the review (Review changes → choose "Comment" or "Request changes").
    33. The PR author makes the requested change locally on the same branch and pushes again — the PR updates automatically.
# back in the partner-recipe-book folder, on the add-french-toast branch
# edit french-toast.md to address the feedback
git add french-toast.md
git commit -m "Address review feedback"
git push
    34. Reviewer approves the PR (Review changes → "Approve").
    35. Either person clicks "Merge pull request" → "Confirm merge". Then "Delete branch" to clean up.
    36. Finally, each person pulls the merged change into their own local main.
git switch main
git pull

Checkpoint — every participant should now have a recipe in their repo that came from their partner, merged through a real pull request.

Wrap-up (10 minutes)
A short discussion is more useful here than another exercise. Suggested questions:
    • What was the moment something clicked for you?
    • What still feels confusing?
    • How is this different from how you currently share code or files?

Then point them at one or two things to try this week so the muscle memory sticks:
    • Put a personal project — even a notes folder — under Git.
    • Try the same flow with a third file format: a .gitignore file. Have them add node_modules/ or .DS_Store and watch Git stop tracking those things.
    • Read one open-source project's CONTRIBUTING.md to see how real projects describe their PR process.
Command cheatsheet — print one per participant
Command	What it does
git init	Turn the current folder into a Git repository.
git status	Show what's changed, staged, and untracked.
git add <file>	Stage a file for the next commit. Use . for everything.
git commit -m "msg"	Save a snapshot of staged changes with a message.
git log --oneline	Show commit history, one line per commit.
git diff	Show unstaged changes line-by-line.
git branch	List branches. Add a name to create one.
git switch <branch>	Move to another branch. Use -c to create and switch.
git merge <branch>	Merge another branch into the current one.
git remote -v	Show configured remote repositories.
git push	Send your commits to the remote.
git pull	Fetch and merge the latest from the remote.
git clone <url>	Download a remote repository to your machine.



Facilitator notes
What goes wrong, and what to do
    • Push rejected — "updates were rejected." Someone else pushed first. Tell them to git pull, then push again.
    • Wrong author name on commits. They forgot to set git config. Fix it for future commits with the config commands from the prereqs section; old commits can stay as-is for the workshop.
    • Detached HEAD state. Usually from git checkout <commit-hash>. Get them back with git switch main.
    • "fatal: not a git repository." They're in the wrong folder. cd into the project folder.
    • Conflict markers committed accidentally. Open the file, remove the markers, commit again.

Pacing tips
    • If you're behind at the break, skip Exercise 1.3 (the conflict one). It's the most discardable section.
    • If you're ahead, have early-finishers help neighbors — peer teaching is the best use of slack time.
    • Resist the urge to explain the staging area in depth. Most people get it from doing add and commit a few times; lectures don't help.

What NOT to cover
Two hours is enough for a working mental model, not for completeness. Save these for a follow-up session: rebasing, cherry-picking, stashing, reflog, submodules, GitHub Actions, forks vs. branches, and rewriting history. Mentioning them as "things you'll learn later" is fine; teaching them now will overload people.