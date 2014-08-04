##我是demo

一个完整的demo，请参照可重复使用的无线点火器

欲呈现的效果为：https://www.zybuluo.com/plantpark/note/24062

各位只需要将md代码提交到github

##github使用教程：
windows https://github.com/JiapengLi/GitTutorial 

mac/linux 等，自行google吧

##github unix cmd 使用教程

###pull request 使用教程

https://www.zybuluo.com/plantpark/note/24419


###第一次使用github，现将仓库clone到本地

git init 

git clone git@github.com:huohuaioio/article.git

###本地仓库增加新文件后如此流程操作

git add *

git commit -m "first commit"

git push -u origin master

###当遇到多人同时更新github仓库时，需要先将github仓库更新到本地，然后在执行第二个步骤。
git fetch --all

git reset --hard origin/master

git pull origin master