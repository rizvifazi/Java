

These are the Steps to follow
1. Create a new repository on GitHub. 
2. Right-click on the project and choose ‘Show in Local Terminal’ - Git Bash
3. (if you don’t see Git Bash, then install it)
4. Initialize the local directory as a Git repository.
$ git init
5. Add the files in your new local repository. This stages them for the first commit.
6. $ git add .
7. # Adds the files in the local repository and stages them for commit.
8. Commit the files that you've staged in your local repository.
9. $ git commit -m "First commit"
10. # Commits the tracked changes and prepares them to be pushed to a remote repository. 
11. Go and copy your remote repository url (it ends in .git)
12. In the Command prompt, add the remote repository url
13. $ git remote add origin (remote-repository)
14. $ git remote -v
Verifies the new remote URL
15. Push the changes in your local repository to GitHub.
16. $ git push origin master
Pushes the changes in your local repository up to the remote repository 