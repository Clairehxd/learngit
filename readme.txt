# First
Git Bash --start at 2018-05-11 0:08
  $ git config --global user.name "Your Name"
  $ git config --global user.email "email@example.com"
  
create a new repository,pwd --print working directory
  $ mkdir learngit
  $ cd learngit
  $ pwd 
init git repository
  $ git init
ls -ah --show the hidden .git

create file: readme.txt --path: learngit
add repository files --truly add files to index (local cache)
  $ git add readme.txt
add repository files -- add repository files from index
  $ git commit -m "wrote a readme file"
diff: add --a file once
      commit --a few files once

historic record
  $ git log
  $ git log --pretty=oneline
return it to the previous version --HEAD^: last version; HEAD^^: last by 2 version
  $ git reset --hard HEAD^
show version
  $ cat readme.txt
return it to the specified version --version no. --Tab
  $ git reset --hard (3628164)
#like a pointer
when u shut down ur computer, u want reset the specified version, u can
  $ git reflog
#use the version no.

working directory and index
.git --git's repository
HEAD is a pointer --> master
-----------------         -----------------repository--------------------
+    working    +   add   +   ----index----  commit   ----master-----   +
+   directory   + ------> +   *           * --------> *             *   +
+               +         +   *           *           *             *   +
+               +         +   *           *           *             *   +
+               +         +   -------------           ---------------   +
-----------------         -----------------------------------------------
show the content of index
  $ git status
  
diff the working directory and repository
  $ git diff HEAD -- readme.txt 
diff both the commit history
  $ git diff (id1) (id2)
  
discard the working directory's alter 
--one is that readme.txt not add to index, return to the repository version
--another is that readme.txt add to index and make another alter, return to the index version
  $ git checkout -- readme.txt
un-index
  $ git reset HEAD readme.txt
  $ git checkout -- readme.txt
working tree clean

rm a working directory file
  $ rm test.txt
rm a repository file
  $ git rm test.txt
or u rm the wrong file
  $ git checkout -- test.txt

local repository relate to origin
push an existing repository from the command line
when u first push master to origin, use '-u' --push master and branchs to origin
https
  $ git remote add origin https://github.com/Clairehxd/learngit.git
ssh
  $ git remote add origin git@github.com:Clairehxd/First.git
  $ git push -u origin master
after, when u push master to origin, use
  $ git push origin master

clone local repository from remote repository
https
  $ git clone https://github.com/Clairehxd/First.git
ssh
  $ git clone git@github.com:Clairehxd/First.git

create a new branch
  $ git checkout -b dev
equivalently --create dev and switch
  $ git branch dev
  $ git checkout dev
show all branchs
  $ git branch
vi readme.txt and
  $ git add readme.txt
  $ git status
  $ git commit -m "branch test"
checkout master
  $ git checkout master
cat readme.txt
  $ cat readme.txt
but find that readme.txt is not modified, because the modification is on branch dev but not master
merge the dev into the current branch
  $ git merge dev
delete dev and show branchs
  $ git branch -d dev
  $ git branch
  
  $ git checkout -b feature1
  $ vi readme.txt
  $ git add readme.txt
  $ git commit -m "AND simple"
  $ git checkout master
  $ vi readme.txt
  $ git add readme.txt
  $ git commit -m "& simple"
  $ git merge feature1
  $ git status
but conflict and the content of readme.txt is
'''
<<<<<<< HEAD
Creating a new branch is quick & simple.
=======
Creating a new branch is quick AND simple.
>>>>>>> feature1
'''
modify as 'Creating a new branch is quick and simple.' and git add, commit
then
  $ git log --graph --pretty=oneline --abbrev-commit
  $ git branch -d feature1
  
  
forbid Fast forward --git merge --no-ff
  $ git merge --no-ff -m "merge with no-ff" dev
  $ git log --graph --pretty=oneline --abbrev-commit
  *   7783885 (HEAD -> master) merge with no-ff
  |\
  | * 25e5ea8 (dev) add merge
  |/
  *   ad855c8 conflict
  |\
  | * 3fa4304 AND simple
  * | 2105e76 & simple“
  |/
  * 3fdc3a4 branch test
  * 5455b4b (origin/master) readme.txt
master is a steady branch and dev is a unsteady branch, everybody works on dev by create his branch, then merge dev into master.

when ur work does not finish and u want to begin another work, u can use this to store it
  $ git stash
  ...
when u finish the second work, u want to continue the first work,
  $ git stash list
  $ git stash pop
git stash pop --as 
  $ git stash apply 
  $ git stash drop
show stash
  $ git stash list
  
 
before merge branch into another branch, u want to delete this branch, u can
  $ git branch -D (branch name)
if merge
  $ git branch -d (branch name)
  
show remote repository
  $ git remote
or in detail
  $ git remote -v
push branch
  $ git push origin (branch name)

delete local repository
  $ rm -rf .git

before clone ur remote repository from  another directory or another computer, u should add shh-key to ur github.com from 
  $ cat ~/.ssh/id_rsa.pub
then
  $ git clone git@github.com:Clairehxd/learngit.git
create remote branch dev for local dev
  $ git checkout -b dev origin/dev
multiplayer working mode is
push ur branch to remote
  $ git push origin branch-name
remote ahead of urs, try to merge both
  $ git pull
if 'git pull' note that "no tracking information", maybe the link between local and remote does not create, use it
  $ git branch --set-upstream branch-name origin/branch-name
  
  
open a new tag
  $ git tag v1.0
show all tags --tags not array by time
  $ git tag
default tag is on the new commit
if u forget to open a tag at the last time, u can
  $ git log --pretty=oneline --abbrev-commit
  $ git tag v0.9 622493
show a tag
  $ git show v1.0
create a tag --'-a' indicate tag-name, '-m' indicate caption
  $ git tag -a v0.1 -m "version 0.1 released" 362816
create a tag --'-s' indicate by private key
  $ git tag -s v0.2 -m "signed version 0.2 released" fec145a
PGP tag
  $ git tag -s <tagname> -m "blablabla..."
delete
  $ git tag -d v1.0
push local tag to remote
  $ git push origin v1.0
push all local tags to remote
  $ git push origin --tags
if local tag has been pushed to remote, delete local
  $ git tag -d v1.0
delete remote
  $ git push origin :refs/tags/v1.0
 
 
 ------------               -------------                 ----------------
 anybody else  ---fork--->  my repository   ---clone--->  local repository
 ------------               -------------                 ----------------

 delete github files but remain local files
  $ git rm --cached test.txt
  $ git commit -m "delete file"
  $ git push
 delete github directory but remain local files
  $ git rm --cached -r directory
  $ git commit -m "delete directory“
  $ git push
