# Github 团队协作入门使用教程

标签（空格分隔）： Github 团队协作

---
使用Github参与开源项目已是众所周知的事情，但作为一个只用过watch和fork的码（码字、码代码）农，要知道，Github同样是非常方便团队协作工具。

当然，你如果能够熟练使用Github就请略过吧，此文针对才接触Github不久的新人。这里用到的主要是Github的fork，clone，commit，push，pull request等命令。

##首先##
团队需要新建一个organization，然后new respository,将团队的代码push到这里。作为成员之一，可直接fork项目到自己的respository。效果如下图所示：plantpark为成员的个人Github账号，article即为respository，下面一行小字显示“forked from huohuaioio/article”,至此，说明团队article项目下的代码已经被自己fork了。

![](http://huohua.qiniudn.com/github2.pic.jpg)


##其次##
需要将位于Github中的article项目复制到本地。由于笔者机子是mac os操作系统，习惯使用unix命令，以下操作均已命令行演示，其他GUI方法自行Google。如何在本地设置Github账号以及key等操作这里不做赘述。

![](http://huohua.qiniudn.com/github7.pic.jpg)

如图，依次新建一个文件夹，githubtest,名称随意。然后git init在这里进行初始化，git clone git@github.com:plantpark/article.git 这个地址，在自己fork后的respository右侧有显示。这样，Github的代码同步到了本地，下面即可在本地新建文件，nano test.txt。test.txt可以用第三方编辑器打开编辑，将文章的markdown代码放入其中，这样一篇文章算是完成了。下面要做的就是通过push将代码同步到Github。git add *,添加此文件夹下所有新建与更改的文件，一种偷懒的做法，git commit -m "test"，写入commit，以便备注每次的push。git push origin master，最后一步，将代码同步到Github。这样，在Github中即可看到自己刚刚提交的代码，https://github.com/plantpark/article。

##最后##

![](http://huohua.qiniudn.com/github3.pic.jpg)

![](http://huohua.qiniudn.com/github4.pic.jpg)

![](http://huohua.qiniudn.com/github5.pic.jpg)

如图所示，在点击respository右侧的pull request，看到一个new pull request 按钮，点击它就能将自己的代码PR到forked的项目中（俗称请求提交？）。写入commit后就直接点creat pull request。

当然，这是作为团队成员自己提交项目代码完成了任务，但是，但变化还未显示到项目代码中，还需要一步，就是项目管理员提交来的pull request 进行merge，添加到项目中。

![](http://huohua.qiniudn.com/github6.pic.jpg)

至此，一个团队协同合作的Githu流程完整呈现出来了，当然，还有些其他的高级功能，这里暂不做表述，可在后面的文章进行详细解说。
