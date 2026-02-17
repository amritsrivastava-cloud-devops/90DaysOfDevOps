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
