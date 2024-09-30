# git-practice

This repo provides instructions for a simple git basics exercise.

# Steps to follow

## Common steps

1. Create a new repository on your github account

2. Clone this new repository by using the `git clone <repo address>` command. You can find the repo address by clicking on the green `Code` button on the main page of the repo.

## Exercise 1: basic git usage

1. Add any file in the cloned folder. Let's say `hello.py` and add any code to it.

2. Ask git to track this file by adding it to git's index: `git add hello.py`

3. Commit your changes `git commit hello.py -m "Add simple python code"`

4. Make another change to `hello.py` and commit again
   
5. Push your changes using `git push`; Voila! If you go back to your repo on github, you should see the commit history of your changes. 

## Exercise 2: branch and PRs

### Exercise 2.1: A simple case merged on the command line

1. `git branch my-new-feature`
2. `git checkout my-new-feature`
3. Create a new file `main.py` and add any code to it
4. Ask git to track this file (remember you are now tracking it on the new branch, not main): `git add main.py`
5. Commit your change `git commit main.py -m "Add main on branch"`
6. Push your change `git push`. Since this is the first time you are pushing to this branch, git will ask you to set upstream. Copy and run the command it provides you to set upstream for this branch (it will look something like this `git push --set-upstream origin my-new-feature`.
7. Go to github and change the branch you are viewing from the top left corner and see how you see the commits from main (until the time you did the branch) plus the new commit you added.
8. Now let's merge our feature branch changes in to the main branch. Since we want to merge things into main, we will check out main first `git checkout main`
9. We will ask git to merge our new branch `git merge new-feature`. 
10. Run a `git status` and see how it tells you that your local main branch is ahead of origin/main and that you need to push your changes. This is because the git merge command created the merge commit when it merged the changes (or more precisely since this case is a fast forward, it just added the new commit to the main history).
11. Push to the remote repo `git push`
12. Go to github and see how the new change(s) you made are part of the main branch history

### Exercise 2.2: A simple case merged through a PR

Let's repeat the above steps but merge things through a Pull Request rather than through the command line.

1. `git status` to make sure we are on the main branch. If we are not, then change to main by running `git checkout main`. Also make sure you have no uncommitted changes.
2. `git pull` just to get in the habit of making sure that your repo is always up to date when you start working.
3. `git branch featureB`
4. `git checkout featureB`
5. Edit `main.py` and make any changes to the code
6. Commit your change `git commit main.py -m "Add changes to main"` (P.S. this is a pretty bad commit message :-) )
6. Push your change `git push`. Since this is the first time you are pushing to this branch, git will ask you to set upstream. Copy and run the command it provides you to set upstream for this branch (it will look something like this `git push --set-upstream origin featureB`.
7. Go to github and change the branch you are viewing from the top left corner and see how you see the commits from main (until the time you did the branch) plus the new commit you added.
8. Now, let's create a pull request to merge the changes we made on the branch into the main branch. Go to the Pull Requests tab on the github repo web page and select "New Pull Request". Make sure the base branch shows `main` (since the repo is the same repo, you won't see a separate repo name selection) and the compare branch shows `featureB`. You should now see the new commit you made in the branch and you can click on "Create Pull Request"
9. On the created pull request, you can see that github tells you that this branch has no conflict with main and can be safely merged. Click on "Merge pull request". Once you are done merging, you can delete the branch through the github interface on the PR
10. Now go to the main branch on github and you will see the that `main.py` has your new changes
11. On your command line, switch to main `git checkout main` and do a `git log` and you will also see the expected commit history there


### Exercise 2.3: Ok, let's create a conflict

1. Assuming we are on main and have the latest updates, create a new branch `git checkout -b featureC` #note that this is a shorthand for creating and checkout out a new branch in one step
2. Change any line in `main.py` and commit and push your changes (you know the drill by now)
3. Now, let's pretend that someone else made changes on the main branch in the meantime. To make this situation real, we will do the following:
	a. `git checkout main`
	b. Make changes to the SAME LINE in `main.py` but create a slightly different variation of this line (e.g., if in step 2, you changed `x = x + 1` to `x = y + 1`, here change the same line to `x = x + 2`
	c. Commit and push your changes
4. Now let's try to merge our changes from featureC into main using the same steps from exercise 2.2:
	a. We go on github and create a new Pull Request asking to merge featureC into main
	b. Now notice how github is refusing to show me the merge button and is asking me to resolve conflicts first? Well, let's resolve the conflict. I will resolve it on the command line as follows
	c. I want to resolve the conflicts on the BRANCH such that github will allow me to merge the pull request into main. Why? I'm the one who's asking to merge my changes on main so I'm responsible for figuring out the conflicts on my new branch and solving them before continuing the PR. So:
5. `git checkout featureC`
6. `git merge featureC` This causes git to list the files that have conflicts. iIn this case, we will see something like `CONFLICT (content): Merge conflict in main.py`
7. So we will open main and find the conflict markers and decide how we want to resolve this conflict. 
8. Once I'm done resolving the conflict, I will ask git to add the file back to its staging/index: `git add main.py`. If I do a `git status` now, git will tell me that i've resolved all conflicts but I'm still merging and need to commit to conclude the merge. So let's commit as follows `git commit -am "Merged changes from main"`
9. Push our changes using `git push` (note this is pushing to our branch)
10. Now go back to your PR on github and refresh. You should see that github now allows you to merge your changes into the main branch! Merge your changes into main.

Note: if you have multiple conflicting files, you will have to resolve all conflicts (steps 7-8).

### BONUS: Exercise 2.4: Merge using rebase

We will mimic the situation in Exercise 2.3 but merge with a rebase. I personally like rebasing better.

1. Repeat steps 1-4 above (With all substeps) but call the branch `featureD`. You should now be at the point where github is blocking you from merging the PR because there is a conflict.
2. We will again try to merge main into featureD. First checkout the feature branch `git checkout featureD`
3. Instead of using git merge, use git rebase `git rebase main`. Git again complains about the conflict and asks you to resolve it.
4. Go to the file it's complaining about and resolve the conflict as usual (in the end, you should have no conflict markers)
5. `git add main.py` this is the file(s) with the conflicts that you resolved
6. ` git rebase --continue`
7. save the commit message 
8. `git push` Now notice how git complains about divergent history? This is because the rebase option rewrites history and git doesn't know what to do. Accordingly, we will force push to the branch `git push -f`
9. If we now go back to the PR, we will see again that github is allowing us to merge

WARNING: USING FORCE PUSH IS DANGEROUS. Unless you really know what you are doing, USE IT ONLY IN THE ABOVE SITUATION ON A FEATURE BRANCH WHEN YOU REBASED FOR A PR. 

Note: if you have multiple conflicting files, you will repeat steps 4-6 until done.
	 
