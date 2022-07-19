Check happy git with r jenny bryan.



## 9 Personal access token for HTTPS. 
When we interact with a remote git server, such as github, we have to include credentials in the request. this proves we are a specific github user, whos allowed to do whatever we're asking to do. 

Git can communicate witha  remote server using one of two protocols, HTTPS or SSH, and the different protocols use different credentials. 
With HTTPS, we will use a **personal access token (PAT)**. 

The password that you use to login to githubs website is not an acceptable credential when talking to github as a git server. This was possible in te past but no more. see https://github.blog/2020-12-15-token-authentication-requirements-for-git-operations/


#### 9.1 TL;DR 
usethis::create_github_token()

scopes recommended. [[gt_repo_scopes]]

Scopes recommended will be automatically pre-selected if you used usethis::create_github_token() for creating your PAT. 

Copy the PAT somewhere and then provide it the next time a Git operation asks for it. 

You could also store the PAT explicitly right now, by calling: 
gitcreds::gitcreds_set()





#### 9.5 HTTPS PAT problems. 

##### 9.5.1 Valid PAT gets stored, but later told the PAT is invalid
!CHECK WEBSITE. 

https://happygitwithr.com/https-pat.html


###### 9.5.1.1 PAT has expired
You are going to be re generating and re storing your PAT on a schedule dictated by its expiration period. By default, once per month. 

When the PAT expires, return to https://github.com/settings/tokens and click on its *Note* (REMEMBER TO LABEL YOUR TOKENS NICELY BY USE CASE). At this point, you can optionallya djust scopes and then click "Regenerate token". You can optionally modify its *Expiration* and then click "Regenerate token" (again). 

Hopefulle it's becoming clear why each token's *Note* is so important (m' not really?'). The actual token may be changing e.g., once a month, but its use case and scopes are much more persistent and stable. 




##### 9.5.1.2 Old GITHUB_PAT in .Renviron

These usethis functions will diagnose this problem:
usethis::gh_token_help()

usethis::git_sitrep()


In the past, it was common to store a PAT as the GITHUB_PAT environment variable in .Renviron. But now, thanks to gircreds and credentials, we can store and retrieve a APT, from R, the same way as command line Git does. 




#### 9.5.3 PAT doesn't persist on Linux 
CHECK WEBSITE





## 15. New project, Github first


#### 15.2 New Rstudio project via git clone. 
There's a big advantage to the "Github first, then Rstudio" workflow: the remote github repo is configured as the `origin` remote for your local repo and your local `main` branch is now tracking the `main` on github. This is a technical but important point about Git. The practical implication is that you are now set up to push and pull. No need to fanny around setting up Git remotes and tracking branches on the command line. 


##### 15.2.1 Optional: peek under the hood
!! CHECK AFTER READING MORE THEORY. 




#### 15.3 Make local changes, save, commit. 
*Make this every time you finish a valuable chunk of work, probably many times a day.*



#### 15.4 Push your local changes to GitHub. 
*Do this a few times a day, but possibly less often than you commit.*


*always pull changes from another collaborator before you push. This is a good habit to avoid git conflict*


#### 15.8 THe end
"lather, rinse, repeat". Do work somewhere: locally or on github. Commit it. Push it or pull it, depending on where you did the work, but get local and remote "synced up". Repeat. 

*Note that in general (and especially in future when collaborating with other deveolperts) you will usually need to pull changed from the remote (github) before pushing the local changes you have made. For this reasons, it's a good idea to try and get into the habit of pulling before you attempt to push. *






## 20 Repo, commit, diff, tag. 

### 20.1 Repos or repositories. 

Git manages the evolution of a set of files - called a *repository or repo* - in a highly structured way. 

Making a project directory an Rstudio Project and Git repository boils down to allowing those applications to leave notes for themselves in hidden files or directories. 

A *commit* makes a snapshot of all the files in the entire project. 


### 20.2 Commits, diffs, and tags

Fundamental concepts of git to the data science workflow: 

- Repository
- Commit
- Diff


**Repo** = A repository or repo is just a directory of files that Git manages holistically. 

**Commit** = A commit functions like a snapshot of all the files in the repo at a specific moment. 

Under the hood, that is not exactly how Git implements things. 

![[Pasted image 20220322185713.png]]

**Diff** = The set of differences between two commits A and B. Diff inspection is how you re explain to yourself how version A differs from version B. Diff inspection is not limited to adjacent commits. You can inspect the diffs between any two commits. 
In fact, Git's notion of any specific verision of a file is as an accumulation of diffs. 
Every later version is stored by Git as the initial version plus all the intervening diffs in the history that affects a file. 

Every time you make a commit you must also write a short *commit message*. Ideally, this conveys the Motivation for the change (remember that the diff will show the content). 

Every commit needs some sort of nickname, so you can indentify it. Git does this automatically, assigning each commit what is called a SHA, a seemmingly random string of 40 letters and numbers (but its not actuall y random but a SHA-1 checksum hash of the commit). Though u will be exposed to these, you don't have to handle them directly very often and when u do, usually the first 7 characters suffice. The commit messages in the last figure are prefixed by such truncated SHAs. You can also designate certain snapshots as special with a **tag**, which is a special name of your choosing. 


**Tag** = a special name (chosen by you) for a commit. In a software project, it is typical to tag a release with its version e.g., "v1.0.3". For a manuscript or analytical project, u might tag the version sumbitted to a journal or transmitted to external collaborators. The last figure shows a tag, "draft-01", associated with the last commit. 




## 21 Git commands

Unless you use the GitHub API, most of the GitHub bits really have to be done from the browser. 

New local git repo from a repo on GitHub: 
git clone https://github.com/franfram/a-repo

Check the remote was clonned succesfully:
git remote --verbose

Stage local changes, commit: 
git add file.txt
git commit --message "A commit message"

Check on the state of the Git world: 
git status
git log
git log --oneline


Compare versions:
git diff

Add a remote to existing local repo: 
git remote add origin https://github.com/franfram/a-repo
git remote --verbose
git remote show origin

Push local `main` to GitHub `main` and have local `main` track `main` on GitHub: 
git push --set-upstream origin main
'm shorter form'
git push -u origin main
m' you only need to set upstream tracking once!'

Regular push: 
git push 
'm the above usually implies (and certainly does in jennys tutorial)'
git push origin main
'm git push (remote-name) (branch-name)'

Pull commits from GitHub: 
git pull

Pull commits and don't let it put you in a merge conflict pickle: 
git pull --ff-only 

Fetch commits:
git fetch

Switch to a branch:
git checkout (branch-name)

Checking remote and branch tracking: 
git remote -v
git remote show origin
git branch --v



Some extra notes by myself 
git pull is shorthand for git fetch followed by git merge FETCH_HEAD. 
More precisely, git pull runs git fetch (fetch means "ir a buscar", fetch means go for and then bring back ,someone or something, for someone) with the given parameters and calls git merge to merge the retrieved branch heads into the current branch.  With --rebase, it runs git rebase instead of git merge. 

git push flag: -u, --set-upstream: for every branch that is up to date or successfully pushed, add upstream (tracking) reference, used by argument-less git-pull and other commands. 


## 22 Branches 

Branching means that you take a detour from the main stream of development and do work without changing the main stream. It allows one or many people to work in parallel without overwriting each other's work. It allows someone working solo to work incrementally on an experimental idea, without jeopardizing the state of the main product. 
Git encourages workflows which create small branches for exploration or new features, often merging them back together quickly. 


### 22.1 Create a new branch

create a new branch:
git branch 

checkout the branch (switch to that branch):
git checkout

To distinguish the branch from the main stream of development, presumably on main, we should give the branch a name, e.g., 'issue-5'
Thus: 
git branch issue-5
git checkout issue-5

Create branch and checkout the branch all at once: 
git checkout -b issue-5

### 22.2 Switching branches
You switch between branches with git checkout

What do u do if you are working on a branch and need to switch, but the work in the current branch is not complete? one options is the Git stash, but generally a better options is to safeguard the current state with a temporary commit. E.g., using "WIP" as the commit message to indicate work in progress. 
git commit --all -m "WIP" ((i guess this is on issue-5 branch))
git checkout main


Then when you come back to the branch and continue your work, you need to undo the temporary commit by *resseting* your state. Specifically, we want a mixed reset. This is "working directory safe", i.e. it does not affect the state of any files. But it does peel off the temporary WIP commit. Belowe, the reference HEAD^ says to roll the commit state back to the parent of the current commit (HEAD).
git checkout issue-5
git reset HEAD^

If this is difficult to remember, or to roll the commit state back to a different previous state, the reference can also be given as the SHA of a specific commit, which you can see via git log. This is wheere i think a graphical Git client can be invaluable, as you can generally right click on the target commit, then select the desired type of reset (e.g., soft, mixed or hard). This is exactly the type of intermediate-to-advanced Git usage that often feels more approachable in a graphical client. 

### 22.3 Merging a branch

Once you have done your work and committed it to the feature branch, you can switch back to main and merge the feature branch. 

git checkout main
git merge issue -5 (the merge will be into the branch you are checked into)


### 22.4 Dealing with conflicts
If both of the branches you are megingn changed the same part of the same file u will get a merge conflict:
```
git merge issue-5
# Auto-merging index.html
# CONFLICT (content): Merge conflict in index.html
# Automatic merge failed; fix conflicts and then commit the result.
```

The first thing to do is **NOT PANIC**. Merge conflicts are not the end of the world and most are relatively small and straightforward to resolve. 

The first step to solving a merge conflict is determining which files are in conflict, which you can do with `git status`:
```
git status
# On branch main
# You have unmerged paths.
#   (fix conflicts and run "git commit")
# 
# Unmerged paths:
#   (use "git add <file>..." to mark resolution)
# 
#     both modified:      index.html
# 
# no changes added to commit (use "git add" and/or "git commit -a")
```

this shows only index.html is unmerged and need to be resolved. 
We can open then open the file to see what lines are in conflict. 
```
<<<<<<< HEAD:index.html
<div id="footer">contact : email.support@github.com</div>
=======
<div id="footer">
 please contact us at support@github.com
</div>
>>>>>>> issue-5:index.html

```
The lines between <<<<< HEAD:index.html and ===== are the content FROM THE BRANCH YOU ARE CUTTENTLY ON (m'i guess that's why it says "HEAD"??). The lines between ===== and >>>>>> are from the feature branch we are merging. 

To resolve the conflict, edit this section until it reflects the state you want in the merged result. Pick one version or the other or create a hybrid. Also remove the conflict markers <<<<<, ===== , and >>>>>/ 
``````
<div id="footer">
please contact us at email.support@github.com
</div>
``````

now run `git add index.html` and `git commit` to finalize the merge. 
CONFLICTS RESOLVED. 

#### 22.4.1 Bailing out
If, during the merge, you get confused about the state of things or make a mistake, use `git merge --abort` to abort the merge and go back to the state prior to running git merge. Then you can try to complete the merge again. 






## 23 Remotes

Remote repositories are versions of your project that are hosted on the internet or another network. A single project can have 1, 2, or even hundreds of remotes. U pull others' changes from remotes and push ur changes to remotes. 

### 23.1 Listing what remotes exist

`git remote -v`

### 23.2 Adding a new remote

`git clone` automatically adds a new remote, so often you do not need to do this manually initially. However, after the initial clone, it is often useful to add additional remotes. 

`git remote add` to add a new remote, e.g.:

`git remote add happygit https://github.com/jennybc/happy-git-with-r.git 

Note: when you add a remote you give it a nickname (here `happygit`), which you can use in git commands in place of the entire URL, e.g.:

`git fetch happygit`

Sidebar on nicknames: there is a strong convention to use `origin` as the nickname of your main remote (m'that is, the main place on the internet where you store your repo'). At this point, it is common for the main remote of a repo to be hosted on GitHub (or GitLab or Bitbucket). It is tempting to use a more descriptiove nickname (such as `github`), but you might find that following the convention is worth it. It makes your setup easier for others to understand and for you to transfer information that you read in documentation, on stack overflow or in blogs. 

A common reason to add a second remote is when you have done a "fork and clone" of a repo and your personal copy (your fork) is set up as the `origin` remote. Eventually you will want to pull changes from the original repository. It is common to use `upstream` as the nickname for this remote. 

`git remote add upstream https://github.com/TRUE_OWNER/REPO.git`


### 23.3 Fetching data from remotes. 

To get new data from a remote use `git fetch <remote_name>`. This retrieves the data locally, but importantly it does not change the sate of your files in any way!. To incorporate the ata fetched into ur repo, you need to merge or rebase ur project with the remote project. 

```
# Fetch the data
git fetch happygit

# Now mege it with our local main
git merge happygit/main main

# git pull is a shotcut which does the above in one command. 
git pull happygit main


```

### 23.4 pushing to remotes
Use `git push <remote? <branch>` to push your local changes to the `<branch>` branch on the `<remote>` remote. 
```
# push my local changes to the origin remote's main branch
git push origin main

# push my local changets to the happygit remote's test branch
git push happygit test

```


### 23.5 Renaming and changing remotes
`git remote rename` to rename a remote: 
`git remote rename happygit hg`

`git remote set-url` can be used to change the URL for a remote. This is sometimes useful if you initiallys et up a remote using HTTPS, but now want to use SSH instead (or vice versa)

`git remote set-url happygit git@github.com:jennybc/happy-git-with-r.git`

One fairly common workflow is you initially cloned a repo on GitHub locally (without forking it), but now want to create your own fork and push changes to it. As described earlier, it is common to call the source repository `upstream` and to call your fork `origin`. So, in this case, you need to first rename the existing remote (from `origin` to `upstream`). Then add your fork as a new remote, with the name `origin`. 

```
git remote rename origin upstream
git remote add origin git@github.com:jimhester/happy-git-with-r.git
```


### 23.6 Upstream tracking branches
A branch can be set on the remote that each of your local remotes corresponds to. `git clone` sets this up automatically, so for your own `main` branch this is not something u will run into. However by default if u create a new branch and try to push  to it u will see something like this: 

```
git checkout -b mybranch #-b creates a new branch, here named `mybranch`
git push 

# fatal: the current branch foo has no upstream branch. 
# To push the current branch and set the remote as upstream user
#
#      git push --set-upstream origin foo

```

You can do as the error message says and explicitly set the upstream branch with `--set-upstream`. However I would recommend instead changing the default behavior of `push` to automatically set the upstream branch to the branch with the same name on the remote. 

U can do this by changing the git `push.default` option to `current`.
`git config --global push.default current`


# Git remote setups

The previous par ended with some basics about Git remotes, such as how to define or rename one. Recall that a Git remote is another copy of the repo, usually living elsewhere (hence the term "remote"), that you can pull changes from or push changes to. Remotes are the foundation for all collaborative Git work. 

But knowing the mechanics of how to add or rename a remote does little good if you don't know why or when to do it. Luckily, we have very strong opinions about how u should set up your remotes, all motivated by getting oyu prepared for smooth, happy collaborative work. 

In this part we describe various remote setups that are common (for better or worse) and what they are good for( or what's wrong with them and how to fix). 


### 24 Common remote setups. 

#### 24.1 No GitHub

![[Pasted image 20220327132448.png]]
How to achieve: 
- Command line Git: `git init`
- With usethis, existing project: `usethis::use_git()`


#### 24.2 Ours (more specifically, yours)
A common next step is to associate a local repo with a copy on GitHub, owned by you. 

![[Pasted image 20220327132634.png]]

A remote named `origin` is configured and you have permission to push to (and pull from) `origin`. (That's why `origin` is colored blue and there are solid arrows going both directions). The `origin` remote on GitHub is what we'll call a **source** repo, meaning it is not a fork (i.e. copy) of anything else on Github. In this case, `origin` is also what we'll call your **primary** repo, meaning it is the proimary remote you interact with on GitHub (for this project). 

How to achieve if the local repo exists first: 
- With usethis: `usethis::use_github()`
- CL Git or Rstudio> you can't complete this task fully from the command line or from Rstudio
	- Command line: `git remote add origin <URL>`
	- Even noew, the setup may no tbe ideal, because upstream tracking relationships are probably not setup, which means you may not be able to push and pull easily. You may need to explicitly configure an upstream tracking branch for one or more local branches. 
	  Next time you want to create a GitHub repo from a local repo, consider using `usethis::use_github()`, which completes all of this setup in one go.


How to achieve if the remote repo exists first: 
- With usethis: `usethis::create_from_github("OWNER/REPO", fork = FALSE)`
- CL: `git clone <URL>`, with the source repo's HTTPS or SSH URL. 

usethis describes this setup as "ours".

### 24.3 Ours
Here's a variation on "ours" that is equivalent in practice. 

![[Pasted image 20220327134122.png]]

A remote named `origin` is configured and u can push to and pull from `origin`. As above, `origin` is a **source** repo, meaning it is not a fork (or copy) of anything else on GitHub. The `origin` remote is however not owned by u. Instead it's owned by another GitHub user or organisation. `origin` is also ur **primary** repo in this setup. 

How does this happen?
1. The source repo is owned by an organisation and ur role in this organisation confers enough power to create repos or to push to this repo. 
2. The owner of the source repo has added u, specifically, as a collaborator to this specific repo. 

How to acheive? this procedure is the same as for the previous "ours" setup. But remember to specify `usethis::use_github(organisation = "ORGNAME")` if u want to create a new repo under an organisation, instead of your personal account. 

usethis describes this setup as "ours".


### 24.4 Theirs. 

This is a setup that many people get themselves into, when it's not actually what they need. It's not broken per se, but it's limiting. 
![[Pasted image 20220327140648.png]]

You cannot push to `origin`, which is both the source repo and ur primary repo. (This is indicated by the orange color of `origin` and the greyed out, dashed "push" arrow. ) `origin` is read-only for you. 

If u are taking a repo for a quick test drive, this configuration is fine. But there's no way to get changes back into the source repo,  since u cannot push to is and u haven't created a fork, which is necessary for a pull request. 

How does this happen?
- `git clone <URL>`  (of an URL that is not urs)
- `usethis::create_from_github("OWNER/REPO", fork = FALSE)` (of an OWNER that is not u)

usethis describes this setup as "theirs"

What if u do want to make a pull request? this means you should have done fork-and-clone instead of clone. If u've made no changes or they're easy to save somewhere temporarily, just start over with a fork-and-clone workflow (see below) and re-introduce ur changes. It is also possible to preserve ur work in a local branch, fork the source repo, re-configure ur remotes, re-sync up with the source repo, and get back on track. But this is much easier to goof up. 
So REMEMBER to use `usethis::create_from_github(fork = TRUE)` in the future!. 


### 24.5 Fork (of theirs). 
This is an ideal setup if u want to make a pull request and generally follow the development of a source repo owned by someone else. 
![[Pasted image 20220327142440.png]]

This shows a succesful "fork-and-clone". Ur local repo can pull changes from the source repo, whici is configured as "upstream", which you cannot push to  (but u can pull from). U have a fork of the source repo (a very special copy, on GitHub) and it is configured as `origin`. `origin` is your primary repo. U can push to and pull from `origin`. U can make a pull request back to the source repo via ur fork. 

How to achieve: 
- `usethis::create_from_github("OWNER/REPO", fork = TRUE)`
- CL Git: you can't complete this task fully from the command line. 
	- Fork the source repo in the browser, capture the HTTPS or SSH URL of **ur fork**, then use `git remote clone <FORK_URL>`. But wait, you are not done! if u stop here, u will have the incomplete setup we refer to as "fork (salvageable)" below. 
	- U still need to add the source repo as the `upstream` remote. Capture the HTTPS or SSH URL of the **source repo**. `git remote add upstream <SOURCE_URL>`.
	- Even then, the setup may not be ideal, because ur local default branch is probably tracking `origin`, not `upstream`, whici is preferable for a fork. 
	  `usethis::create_from_github()` completes all of this setup in one go. 

### 24.6 Fork (of ours). 
This is a less common variation on  the fork setup. 
![[Pasted image 20220327144158.png]]
In this case, u have permission to push to the source repo, but u elect to create a personal fork anyway. Certain project favor this approach and it offers maximum development flexibility for advance dusers. Howeer, most users are better served by the simpler "our" setup in this case. 
How to achieve: 
- In general, it's the same as the regular fork setup above. 
- with usethis, make sure to explicitly specify fork = TRUE, `usethis::create_from_github("OWNER/REPO", fork = TRUE)`

usethis describes this setup as "fork"

### Fork (salvageable)
Here is one last fork setup that's sub-optimal, but can be salvaged.
![[Pasted image 20220327144458.png]]
This is what happens when u do a fork-and-clone and u only do fork-and-clone. What's missing is a connection back to the source repo. 

How does this happen? 
- Cloning ur own fork, `git clone` in the shell, and then stopping there. 

If u only plant to make one pull request, this setup is fine. When the exchange is done, delete ur local repo and ur fork and move on with ur life. U can always re-fork in the future. But if ur pull request stays open for a while or if u plan to make repeated contributions, u'll need to pull ongoing deveolpments in the source repo into ur local copy. 

Fix this by adding the source repo as ur `upstream` remote. Capture the HTTP or SSH URL of the **source repo** and then: 
- usethis: `usethis::use_git_remote(name = "upstream", url = "SOURCE_URL")`
- CL Git: `git remote add upstream <SOURCE_URL>`

!!!
Even now, the setup may not be ideal, because ur local default branch is probably tracking `origin`, not `upstream`, which is preferable for a fork. Next time u do a fork-and-clone, consider using `usethis::create_from_github(fork = TRUE)` instead, which completes all of this setup in one go. 

usethis describes this setup as "fork_upstream_is_not_origin_parent"



### 25 Equivocal remote setups
