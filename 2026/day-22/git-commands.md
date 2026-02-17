# GIT COMMANDS 

| COMMAND | DESCRIPTION |
|--------|------|
| sudo apt install git |
| git --version |
| git init (initialize git repo)| 
| git add (add from untraced to staged) |
| git rm --cached filename (move from staged to untraced) |
| git commit -m "messge" (commited once can't removed permanently , will be recovered if deleted) |
| git log (shows hash username email ) |
| git status |
| git restore | 

```

git config --global user.name amritsrivastava-cloud-devops
git config --global user.email amrits.cloud@gmail.com
```
```
git branch
git branch branch-name
git checkout branch-name
git checkout -b branch-name
git switch branch-name
git switch -c branch-name
git branch -D branch-name
```
```
git remote set-url origin <sshkey-link>
git remote add origin https://personalacesstoken@github.com/amritsrivastava-cloud-devops/devops-git-practice.git
git push origin main
git pull origin main

```
```
git clone https://github.com/amritsrivastava-cloud-devops/linux-utility-gcp.git
git remote -v
git remote add upstream https://github.com/rahulwagh/linux-utility.git
git fetch upstream
git branch
git branch -a
git merge upstream/main
git push -u origin main
```
### git demo for setting url for personal acess token 
<img width="2328" height="1098" alt="image" src="https://github.com/user-attachments/assets/689a34db-6ade-41f2-923d-60c04673295d" />

### git demo for setting url for ssh

<img width="2100" height="1252" alt="image" src="https://github.com/user-attachments/assets/872bae39-dfc5-4f7f-9c48-f425d4b948dc" />
<img width="2236" height="1450" alt="image" src="https://github.com/user-attachments/assets/6e460734-2d73-412c-bc12-524074515eb0" />


## git merge 
```bash
ubuntu@ip-172-31-3-172:~/shell-scripts/day24/devops-nginx-demo$ git log
commit b8df475faec7b55257249c5f9cad695bbd563f24 (HEAD -> main, origin/main)
Author: amritsrivastava-cloud-devops <amrits.cloud@gmail.com>
Date:   Tue Feb 17 03:04:28 2026 +0000

    ssh modifiy

commit 99eb4af7cc520933a02179093bcf20ef8ed62259
Author: amritsrivastava-cloud-devops <amrits.cloud@gmail.com>
Date:   Tue Feb 17 03:00:37 2026 +0000

    using ssh

commit 677a47d36e126584549c92a5b76582512fee7c3a
Author: amritsrivastava-cloud-devops <amrits.cloud@gmail.com>
Date:   Tue Feb 17 02:42:40 2026 +0000

    nginx commit
ubuntu@ip-172-31-3-172:~/shell-scripts/day24/devops-nginx-demo$ git log --oneline
b8df475 (HEAD -> main, origin/main) ssh modifiy
99eb4af using ssh
677a47d nginx commit
ubuntu@ip-172-31-3-172:~/shell-scripts/day24/devops-nginx-demo$ git branch 
* main
ubuntu@ip-172-31-3-172:~/shell-scripts/day24/devops-nginx-demo$ git checkout -b dev
Switched to a new branch 'dev'
ubuntu@ip-172-31-3-172:~/shell-scripts/day24/devops-nginx-demo$ git branch dev
fatal: a branch named 'dev' already exists
ubuntu@ip-172-31-3-172:~/shell-scripts/day24/devops-nginx-demo$ git branch
* dev
  main
ubuntu@ip-172-31-3-172:~/shell-scripts/day24/devops-nginx-demo$ ls
README.md
ubuntu@ip-172-31-3-172:~/shell-scripts/day24/devops-nginx-demo$ vi install_nginx.sh
ubuntu@ip-172-31-3-172:~/shell-scripts/day24/devops-nginx-demo$ chmod 764  install_nginx.sh 
ubuntu@ip-172-31-3-172:~/shell-scripts/day24/devops-nginx-demo$ ./install_nginx.sh 
Hit:1 http://us-east-1.ec2.archive.ubuntu.com/ubuntu noble InRelease
Get:2 http://us-east-1.ec2.archive.ubuntu.com/ubuntu noble-updates InRelease [126 kB]
Get:3 http://us-east-1.ec2.archive.ubuntu.com/ubuntu noble-backports InRelease [126 kB]
Get:4 http://security.ubuntu.com/ubuntu noble-security InRelease [126 kB]
Get:5 http://us-east-1.ec2.archive.ubuntu.com/ubuntu noble-updates/main amd64 Packages [1754 kB]
Get:6 http://us-east-1.ec2.archive.ubuntu.com/ubuntu noble-updates/main Translation-en [326 kB]
Get:7 http://us-east-1.ec2.archive.ubuntu.com/ubuntu noble-updates/main amd64 Components [175 kB]
Get:8 http://us-east-1.ec2.archive.ubuntu.com/ubuntu noble-updates/main amd64 c-n-f Metadata [16.5 kB]
Get:9 http://us-east-1.ec2.archive.ubuntu.com/ubuntu noble-updates/universe amd64 Packages [1555 kB]
Get:10 http://us-east-1.ec2.archive.ubuntu.com/ubuntu noble-updates/universe Translation-en [314 kB]
Get:11 http://us-east-1.ec2.archive.ubuntu.com/ubuntu noble-updates/universe amd64 Components [386 kB]
Get:12 http://us-east-1.ec2.archive.ubuntu.com/ubuntu noble-updates/universe amd64 c-n-f Metadata [32.1 kB]
Get:13 http://us-east-1.ec2.archive.ubuntu.com/ubuntu noble-updates/restricted amd64 Packages [2621 kB]
Get:14 http://us-east-1.ec2.archive.ubuntu.com/ubuntu noble-updates/restricted Translation-en [603 kB]
Get:15 http://us-east-1.ec2.archive.ubuntu.com/ubuntu noble-updates/restricted amd64 Components [212 B]
Get:16 http://us-east-1.ec2.archive.ubuntu.com/ubuntu noble-updates/multiverse amd64 Components [940 B]
Get:17 http://us-east-1.ec2.archive.ubuntu.com/ubuntu noble-backports/main amd64 Components [7312 B]
Get:18 http://us-east-1.ec2.archive.ubuntu.com/ubuntu noble-backports/universe amd64 Components [10.5 kB]
Get:19 http://us-east-1.ec2.archive.ubuntu.com/ubuntu noble-backports/restricted amd64 Components [216 B]
Get:20 http://us-east-1.ec2.archive.ubuntu.com/ubuntu noble-backports/multiverse amd64 Components [212 B]
Get:21 http://security.ubuntu.com/ubuntu noble-security/main amd64 Packages [1451 kB]
Get:22 http://security.ubuntu.com/ubuntu noble-security/main Translation-en [235 kB]
Get:23 http://security.ubuntu.com/ubuntu noble-security/main amd64 Components [21.5 kB]
Get:24 http://security.ubuntu.com/ubuntu noble-security/universe amd64 Packages [933 kB]
Get:25 http://security.ubuntu.com/ubuntu noble-security/universe Translation-en [213 kB]
Get:26 http://security.ubuntu.com/ubuntu noble-security/universe amd64 Components [74.2 kB]
Get:27 http://security.ubuntu.com/ubuntu noble-security/universe amd64 c-n-f Metadata [19.9 kB]
Get:28 http://security.ubuntu.com/ubuntu noble-security/restricted amd64 Packages [2457 kB]
Get:29 http://security.ubuntu.com/ubuntu noble-security/restricted Translation-en [566 kB]
Get:30 http://security.ubuntu.com/ubuntu noble-security/restricted amd64 Components [208 B]
Get:31 http://security.ubuntu.com/ubuntu noble-security/multiverse amd64 Components [212 B]
Fetched 14.2 MB in 3s (5640 kB/s)                                
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
50 packages can be upgraded. Run 'apt list --upgradable' to see them.
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
0 upgraded, 0 newly installed, 0 to remove and 50 not upgraded.
Synchronizing state of nginx.service with SysV service script with /usr/lib/systemd/systemd-sysv-install.
Executing: /usr/lib/systemd/systemd-sysv-install enable nginx
nginx installed works 
ubuntu@ip-172-31-3-172:~/shell-scripts/day24/devops-nginx-demo$ git add install_nginx.sh 
ubuntu@ip-172-31-3-172:~/shell-scripts/day24/devops-nginx-demo$ git commit -m "chore : minor changes to nginx script "
[dev 4240cbf] chore : minor changes to nginx script
 1 file changed, 11 insertions(+)
 create mode 100755 install_nginx.sh
ubuntu@ip-172-31-3-172:~/shell-scripts/day24/devops-nginx-demo$ vi install_nginx.sh 
ubuntu@ip-172-31-3-172:~/shell-scripts/day24/devops-nginx-demo$ git add install_nginx.sh 
ubuntu@ip-172-31-3-172:~/shell-scripts/day24/devops-nginx-demo$ git commit -m "chore : new change major"
[dev 190b9c8] chore : new change major
 1 file changed, 1 insertion(+), 1 deletion(-)
ubuntu@ip-172-31-3-172:~/shell-scripts/day24/devops-nginx-demo$ git log --oneline
190b9c8 (HEAD -> dev) chore : new change major
4240cbf chore : minor changes to nginx script
b8df475 (origin/main, main) ssh modifiy
99eb4af using ssh
677a47d nginx commit
ubuntu@ip-172-31-3-172:~/shell-scripts/day24/devops-nginx-demo$ git switch main
Switched to branch 'main'
Your branch is up to date with 'origin/main'.
ubuntu@ip-172-31-3-172:~/shell-scripts/day24/devops-nginx-demo$ git log --oneline
b8df475 (HEAD -> main, origin/main) ssh modifiy
99eb4af using ssh
677a47d nginx commit
ubuntu@ip-172-31-3-172:~/shell-scripts/day24/devops-nginx-demo$ git merge dev
Updating b8df475..190b9c8
Fast-forward
 install_nginx.sh | 11 +++++++++++
 1 file changed, 11 insertions(+)
 create mode 100755 install_nginx.sh
ubuntu@ip-172-31-3-172:~/shell-scripts/day24/devops-nginx-demo$ git log --oneline
190b9c8 (HEAD -> main, dev) chore : new change major
4240cbf chore : minor changes to nginx script
b8df475 (origin/main) ssh modifiy
99eb4af using ssh
677a47d nginx commit
ubuntu@ip-172-31-3-172:~/shell-scripts/day24/devops-nginx-demo$ git branch
  dev
* main


```

## if you commit some changes in dev branch and in main branch for both commit it will be confugin 

```bash
ubuntu@ip-172-31-3-172:~/shell-scripts/day24$ ls
devops-nginx-demo  index.nginx-debian.html
ubuntu@ip-172-31-3-172:~/shell-scripts/day24$ cd devops-nginx-demo/
ubuntu@ip-172-31-3-172:~/shell-scripts/day24/devops-nginx-demo$ ls
README.md  index.nginx-debian.html  install_nginx.sh
ubuntu@ip-172-31-3-172:~/shell-scripts/day24/devops-nginx-demo$ git switch dev
Switched to branch 'dev'
ubuntu@ip-172-31-3-172:~/shell-scripts/day24/devops-nginx-demo$ git add index.nginx-debian.html 
ubuntu@ip-172-31-3-172:~/shell-scripts/day24/devops-nginx-demo$ git commit -m "index html file "
[dev f452a37] index html file
 1 file changed, 1 insertion(+)
 create mode 100644 index.nginx-debian.html
ubuntu@ip-172-31-3-172:~/shell-scripts/day24/devops-nginx-demo$ git push origin dev
Enumerating objects: 4, done.
Counting objects: 100% (4/4), done.
Delta compression using up to 2 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 356 bytes | 356.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
remote: 
remote: Create a pull request for 'dev' on GitHub by visiting:
remote:      https://github.com/amritsrivastava-cloud-devops/devops-nginx-demo/pull/new/dev
remote: 
To github.com:amritsrivastava-cloud-devops/devops-nginx-demo.git
 * [new branch]      dev -> dev
ubuntu@ip-172-31-3-172:~/shell-scripts/day24/devops-nginx-demo$ git branch
* dev
  main
ubuntu@ip-172-31-3-172:~/shell-scripts/day24/devops-nginx-demo$ git pull
remote: Enumerating objects: 1, done.
remote: Counting objects: 100% (1/1), done.
remote: Total 1 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
Unpacking objects: 100% (1/1), 940 bytes | 940.00 KiB/s, done.
From github.com:amritsrivastava-cloud-devops/devops-nginx-demo
   190b9c8..853b699  main       -> origin/main
There is no tracking information for the current branch.
Please specify which branch you want to merge with.
See git-pull(1) for details.

    git pull <remote> <branch>

If you wish to set tracking information for this branch you can do so with:

    git branch --set-upstream-to=origin/<branch> dev

ubuntu@ip-172-31-3-172:~/shell-scripts/day24/devops-nginx-demo$ git status --oneline
error: unknown option `oneline'
usage: git status [<options>] [--] [<pathspec>...]

    -v, --[no-]verbose    be verbose
    -s, --[no-]short      show status concisely
    -b, --[no-]branch     show branch information
    --[no-]show-stash     show stash information
    --[no-]ahead-behind   compute full ahead/behind values
    --[no-]porcelain[=<version>]
                          machine-readable output
    --[no-]long           show status in long format (default)
    -z, --[no-]null       terminate entries with NUL
    -u, --[no-]untracked-files[=<mode>]
                          show untracked files, optional modes: all, normal, no. (Default: all)
    --[no-]ignored[=<mode>]
                          show ignored files, optional modes: traditional, matching, no. (Default: traditional)
    --[no-]ignore-submodules[=<when>]
                          ignore changes to submodules, optional when: all, dirty, untracked. (Default: all)
    --[no-]column[=<style>]
                          list untracked files in columns
    --no-renames          do not detect renames
    --renames             opposite of --no-renames
    -M, --find-renames[=<n>]
                          detect renames, optionally set similarity index

ubuntu@ip-172-31-3-172:~/shell-scripts/day24/devops-nginx-demo$ git log --loneline
fatal: unrecognized argument: --loneline
ubuntu@ip-172-31-3-172:~/shell-scripts/day24/devops-nginx-demo$ git log --oneline
f452a37 (HEAD -> dev, origin/dev) index html file
190b9c8 (main) chore : new change major
4240cbf chore : minor changes to nginx script
b8df475 ssh modifiy
99eb4af using ssh
677a47d nginx commit
ubuntu@ip-172-31-3-172:~/shell-scripts/day24/devops-nginx-demo$ git switch main
Switched to branch 'main'
Your branch is behind 'origin/main' by 2 commits, and can be fast-forwarded.
  (use "git pull" to update your local branch)
ubuntu@ip-172-31-3-172:~/shell-scripts/day24/devops-nginx-demo$ git pull origin main
From github.com:amritsrivastava-cloud-devops/devops-nginx-demo
 * branch            main       -> FETCH_HEAD
Updating 190b9c8..853b699
Fast-forward
 index.nginx-debian.html | 1 +
 1 file changed, 1 insertion(+)
 create mode 100644 index.nginx-debian.html
ubuntu@ip-172-31-3-172:~/shell-scripts/day24/devops-nginx-demo$ git log --oneline
853b699 (HEAD -> main, origin/main) Merge pull request #1 from amritsrivastava-cloud-devops/dev
f452a37 (origin/dev, dev) index html file
190b9c8 chore : new change major
4240cbf chore : minor changes to nginx script
b8df475 ssh modifiy
99eb4af using ssh
677a47d nginx commit
ubuntu@ip-172-31-3-172:~/shell-scripts/day24/devops-nginx-demo$ vi in
ubuntu@ip-172-31-3-172:~/shell-scripts/day24/devops-nginx-demo$ vi index.nginx-debian.html 
ubuntu@ip-172-31-3-172:~/shell-scripts/day24/devops-nginx-demo$ git add index.nginx-debian.html 
ubuntu@ip-172-31-3-172:~/shell-scripts/day24/devops-nginx-demo$ git commit -m "chore : added minor change "
[main 30af3c3] chore : added minor change
 1 file changed, 3 insertions(+)
ubuntu@ip-172-31-3-172:~/shell-scripts/day24/devops-nginx-demo$ git checkout dev
Switched to branch 'dev'
ubuntu@ip-172-31-3-172:~/shell-scripts/day24/devops-nginx-demo$ vi install_nginx.sh 
ubuntu@ip-172-31-3-172:~/shell-scripts/day24/devops-nginx-demo$ git add install_nginx.sh 
ubuntu@ip-172-31-3-172:~/shell-scripts/day24/devops-nginx-demo$ git commit -m "chore minor change in install script"
[dev a6b4646] chore minor change in install script
 1 file changed, 1 insertion(+), 1 deletion(-)
ubuntu@ip-172-31-3-172:~/shell-scripts/day24/devops-nginx-demo$ git swtich main
git: 'swtich' is not a git command. See 'git --help'.

The most similar command is
	switch
ubuntu@ip-172-31-3-172:~/shell-scripts/day24/devops-nginx-demo$ git switch main
Switched to branch 'main'
Your branch is ahead of 'origin/main' by 1 commit.
  (use "git push" to publish your local commits)
ubuntu@ip-172-31-3-172:~/shell-scripts/day24/devops-nginx-demo$ git log --oneline
30af3c3 (HEAD -> main) chore : added minor change
853b699 (origin/main) Merge pull request #1 from amritsrivastava-cloud-devops/dev
f452a37 (origin/dev) index html file
190b9c8 chore : new change major
4240cbf chore : minor changes to nginx script
b8df475 ssh modifiy
99eb4af using ssh
677a47d nginx commit
ubuntu@ip-172-31-3-172:~/shell-scripts/day24/devops-nginx-demo$ git switch dev
Switched to branch 'dev'
ubuntu@ip-172-31-3-172:~/shell-scripts/day24/devops-nginx-demo$ git log --oneline 
a6b4646 (HEAD -> dev) chore minor change in install script
f452a37 (origin/dev) index html file
190b9c8 chore : new change major
4240cbf chore : minor changes to nginx script
b8df475 ssh modifiy
99eb4af using ssh
677a47d nginx commit
ubuntu@ip-172-31-3-172:~/shell-scripts/day24/devops-nginx-demo$ 
```
## statsh and stash pop 

```bash
ubuntu@ip-172-31-3-172:~/shell-scripts/day24/devops-nginx-demo$ git checkout main
Already on 'main'
Your branch is ahead of 'origin/main' by 1 commit.
  (use "git push" to publish your local commits)
ubuntu@ip-172-31-3-172:~/shell-scripts/day24/devops-nginx-demo$ ls
README.md  index.nginx-debian.html  install_nginx.sh
ubuntu@ip-172-31-3-172:~/shell-scripts/day24/devops-nginx-demo$ git branch 
  dev
* main
ubuntu@ip-172-31-3-172:~/shell-scripts/day24/devops-nginx-demo$ vi index.nginx-debian.html 
ubuntu@ip-172-31-3-172:~/shell-scripts/day24/devops-nginx-demo$ git switch dev 
M	index.nginx-debian.html
Switched to branch 'dev'
ubuntu@ip-172-31-3-172:~/shell-scripts/day24/devops-nginx-demo$ vi index.nginx-debian.html 
ubuntu@ip-172-31-3-172:~/shell-scripts/day24/devops-nginx-demo$ git switch main 
M	index.nginx-debian.html
Switched to branch 'main'
Your branch is ahead of 'origin/main' by 1 commit.
  (use "git push" to publish your local commits)
ubuntu@ip-172-31-3-172:~/shell-scripts/day24/devops-nginx-demo$ git stash index.nginx-debian.html
fatal: subcommand wasn't specified; 'push' can't be assumed due to unexpected token 'index.nginx-debian.html'
ubuntu@ip-172-31-3-172:~/shell-scripts/day24/devops-nginx-demo$ git status
On branch main
Your branch is ahead of 'origin/main' by 1 commit.
  (use "git push" to publish your local commits)

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   index.nginx-debian.html

no changes added to commit (use "git add" and/or "git commit -a")
ubuntu@ip-172-31-3-172:~/shell-scripts/day24/devops-nginx-demo$ git switch dev
M	index.nginx-debian.html
Switched to branch 'dev'
ubuntu@ip-172-31-3-172:~/shell-scripts/day24/devops-nginx-demo$ cat index.nginx-debian.html 
this is demo 1


second time change


i am doing some minor changes . 
ubuntu@ip-172-31-3-172:~/shell-scripts/day24/devops-nginx-demo$ git stash 
Saved working directory and index state WIP on dev: bc11e40 chore minor change in install script
ubuntu@ip-172-31-3-172:~/shell-scripts/day24/devops-nginx-demo$ git status
On branch dev
nothing to commit, working tree clean
ubuntu@ip-172-31-3-172:~/shell-scripts/day24/devops-nginx-demo$ git checkout main
Switched to branch 'main'
Your branch is ahead of 'origin/main' by 1 commit.
  (use "git push" to publish your local commits)
ubuntu@ip-172-31-3-172:~/shell-scripts/day24/devops-nginx-demo$ git status
On branch main
Your branch is ahead of 'origin/main' by 1 commit.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean
ubuntu@ip-172-31-3-172:~/shell-scripts/day24/devops-nginx-demo$ cat index.nginx-debian.html 
this is demo 1


second time change 
ubuntu@ip-172-31-3-172:~/shell-scripts/day24/devops-nginx-demo$ vi index.nginx-debian.html 
ubuntu@ip-172-31-3-172:~/shell-scripts/day24/devops-nginx-demo$ git stash pop
On branch main
Your branch is ahead of 'origin/main' by 1 commit.
  (use "git push" to publish your local commits)

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   index.nginx-debian.html

no changes added to commit (use "git add" and/or "git commit -a")
Dropped refs/stash@{0} (f591db6444a319ecdc4075531b49574b2e1770ad)
ubuntu@ip-172-31-3-172:~/shell-scripts/day24/devops-nginx-demo$ cat index.nginx-debian.html 
this is demo 1


second time change


i am doing some minor changes . 
ubuntu@ip-172-31-3-172:~/shell-scripts/day24/devops-nginx-demo$ git switch dev 
M	index.nginx-debian.html
Switched to branch 'dev'
ubuntu@ip-172-31-3-172:~/shell-scripts/day24/devops-nginx-demo$ cat index.nginx-debian.html 
this is demo 1


second time change


i am doing some minor changes . 
ubuntu@ip-172-31-3-172:~/shell-scripts/day24/devops-nginx-demo$ 
```
