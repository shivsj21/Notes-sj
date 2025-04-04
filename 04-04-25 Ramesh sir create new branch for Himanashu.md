## Create New Branch and pull from dev branch
cd /var/www/html/anshu/sjpanel.com/public_html/sjpanel-live/
git branch
git status
git add .
git commit -m "file Changes"
git push
git pull
git checkout dev
git checkout -b himanshu-112
git branch
git pull
git branch --set-upstream-to=origin/himanshu-112      //Sets the upstream for himanshu-112 to track a remote branch 
git branch

