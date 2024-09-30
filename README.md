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

### Exercise 2.1: A simple case

1. `git branch my-new-feature`
2. `git checkout my-new-feature`
3. Create a new file `main.py` and add any code to it
4. Ask git to track this file (remember you are now tracking it on the new branch, not main): `git add main.py`
5. Commit your change `git commit main.py -m "Add main on branch"`
6. Push your change `git push`. Since this is the first time you are pushing to this branch, git will ask you to set upstream. Copy and run the command it provides you to set upstream for this branch.
7. Go to github and change the branch from the top left corner and see how you see the history from main plus the new commit you added
8. Let's create a pull request on 

### Exercise 2.2: Ok, let's create a conflict

1. Assuming you haven't switched branchs yet, go `
