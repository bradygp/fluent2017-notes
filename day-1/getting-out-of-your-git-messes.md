# Git-ing out of your Git messes
### Katie Sylor-Miller, @ksylor, @ohshitgit

## Fundamental Concepts
### Commit
 * snapshot of whole repo
 * every single commit is garunteed unique

each commit is a link list is the data and a pointer back to its parent. 

Branches are just a pointer to a single commit. 
The HEAD is another kind of reference, it points to the tip of the current working branch. It is a symbolic reference. 
It points to a branch, not to a commit (it is a reference to a reference)
There is only 1 head per repo, it lives on the local machine and is not shared.

When you checkout a branch, HEAD now points to the tip of that branch, not master.

### History
History is a directed acyclic graph. Youre not going to hit the same node twice, and it is directed. 

### Environments
Git is decentralized, there is a remote/origin server where the shared git repo is stored.
On the local machine there is a local copy of the git repo (lives in the .git repo)
There is a staging/index area this represnts all the files in your repo at a point in time
workspace is the file structure where all the changes occur

`git status` is your BFF, you should run it before doing anything, it is super helpful.

### Rebase
`git pull --rebase` is used to keep things more linear when commiting between things like origin/master and master branches.
`git log` is awesome, look into it
`git reflog` is a record of all the actions that change the state of the git tree

git show HEAD@{8} 
git checkout HEAD@{8} will checkout a previous state, read-only as detached head

### Changing History
3 different types of rests, soft/mixed/hard

reset is great for fixing local changes, but never do that for something that needs to make it into a remote repo

use `git revert` to to fix things in a remote repo


  1. Always be commiting. they are cheap and easy, no reason to not always be doing them. They are like a safety net.
    * smaller diffs are easier to review and fix if needed.
  2. setup command line to show you which branch you are on
  3. git status is your BGG
  4. understand how staging works

git commit --ammend will allow you to edit commits
  * you can edit the commit message
  * you can add files to the commit
  * do not do this after the commit has already been pushed

Merge v Rebase
If someone has touched the same files as you, you would have to resolve merge conflicts. But with rebase, you changes would just get applied on top.

`git diff --check` will give you a warning if there are any conflict markings in your files (like the ones added in merge conflicts)
It might be possible to add a git hook to check for this
