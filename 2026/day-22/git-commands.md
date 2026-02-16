# GIT COMMANDS 

| COMMAND | DESCRIPTION |
sudo apt install git   
git --version
git init (initialize git repo)
git add (add from untraced to staged)
git rm --cached filename (move from staged to untraced)
git commit -m "messge" (commited once can't removed permanently , will be recovered if deleted)
git log (shows hash username email )
git status 
git restore

git config --global user.name amritsrivastava-cloud-devops
git config --global user.email amrits.cloud@gmail.com

git branch
git branch branch-name
git checkout branch-name
git checkout -b branch-name
git switch branch-name
git switch -c branch-name
git branch -D branch-name 

git remote add origin https://personalacesstoken@github.com/amritsrivastava-cloud-devops/devops-git-practice.git
git push origin main
git pull origin main
git clone https://github.com/amritsrivastava-cloud-devops/linux-utility-gcp.git
git remote -v
git remote add upstream https://github.com/rahulwagh/linux-utility.git
git fetch upstream
git branch
git branch -a
git merge upstream/main
git push -u origin main

