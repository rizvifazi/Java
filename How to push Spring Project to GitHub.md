
# How to push Spring Project to GitHub


#### 1. Initialize a git repo locally with "==main==" branch, if not specified will create the branch as "master"
```bash

acer@RIZVI MINGW64 ~/eclipse-workspace/SpringProfiles
$ git init -b main
Initialized empty Git repository in C:/Users/acer/eclipse-workspace/SpringProfiles/.git/
```

#### 2. Stage all the changes
```shell
acer@RIZVI MINGW64 ~/eclipse-workspace/SpringProfiles (main)
$ git add .
warning: in the working copy of '.gitignore', LF will be replaced by CRLF the next time Git touches it
warning: in the working copy of '.mvn/wrapper/maven-wrapper.properties', LF will be replaced by CRLF the next time Git touches it
warning: in the working copy of 'mvnw', LF will be replaced by CRLF the next time Git touches it
warning: in the working copy of 'mvnw.cmd', LF will be replaced by CRLF the next time Git touches it
warning: in the working copy of 'pom.xml', LF will be replaced by CRLF the next time Git touches it
warning: in the working copy of 'src/main/java/com/example/SpringProfiles/ServletInitializer.java', LF will be replaced by CRLF the next time Git touches it
warning: in the working copy of 'src/main/java/com/example/SpringProfiles/SpringProfilesApplication.java', LF will be replaced by CRLF the next time Git touches it
warning: in the working copy of 'src/main/resources/application.properties', LF will be replaced by CRLF the next time Git touches it
warning: in the working copy of 'src/test/java/com/example/SpringProfiles/SpringProfilesApplicationTests.java', LF will be replaced by CRLF the next time Git touches it
```

#### 3. Commit all the changes
```shell
acer@RIZVI MINGW64 ~/eclipse-workspace/SpringProfiles (main)
$ git commit -m "First commit"
[main (root-commit) a6a7a51] First commit
 10 files changed, 593 insertions(+)
 create mode 100644 .gitignore
 create mode 100644 .mvn/wrapper/maven-wrapper.properties
 create mode 100644 mvnw
 create mode 100644 mvnw.cmd
 create mode 100644 pom.xml
 create mode 100644 src/main/java/com/example/SpringProfiles/ServletInitializer.java
 create mode 100644 src/main/java/com/example/SpringProfiles/SpringProfilesApplication.java
 create mode 100644 src/main/resources/application.properties
 create mode 100644 src/main/webapp/WEB-INF/views/index.jsp
 create mode 100644 src/test/java/com/example/SpringProfiles/SpringProfilesApplicationTests.java

```

#### 4. Create a GitHub repo with a Project Name and copy the url. 
> DO NOT add any readme or license file, which would create a commit in itself a would cause merge conflicts when trying to push the local repo.


#### 5. Set the created repo url as the origin.
```shell
acer@RIZVI MINGW64 ~/eclipse-workspace/SpringProfiles (main)
$ git remote add origin https://github.com/rizvifazi/SpringProfiles.git
```

#### 6. Switch to Main branch
```shell
acer@RIZVI MINGW64 ~/eclipse-workspace/SpringProfiles (main)
$ git branch -M main
```

#### 7. Push the commits
```shell
acer@RIZVI MINGW64 ~/eclipse-workspace/SpringProfiles (main)
$ git push -u origin main
Enumerating objects: 29, done.
Counting objects: 100% (29/29), done.
Delta compression using up to 8 threads
Compressing objects: 100% (17/17), done.
Writing objects: 100% (29/29), 9.21 KiB | 3.07 MiB/s, done.
Total 29 (delta 1), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (1/1), done.
To https://github.com/rizvifazi/SpringProfiles.git
 * [new branch]      main -> main
branch 'main' set up to track 'origin/main'.
```



## Alternate (with master branch conflicts)
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


