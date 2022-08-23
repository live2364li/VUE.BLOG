---
title: Solo的评论/回复邮件提醒功能设置（QQ邮箱）
copyright_author_href: https://layne666.cn
cover: https://pan.layne666.cn/images/2021/12/02/hZ4BBYtEjY.png
date: 2019-01-01 22:29:41
updated: 2019-02-08 17:19:25
categories: 
  - Solo
tags: 
  - Solo
---

话说我今天看到solo系统有**评论/回复邮件提醒**功能，然后我自己尝试回复一下我小号发的评论，评论是回复成功了，但是邮件没发出去！

然后我就去找solo的[用户指南](https://hacpai.com/article/1492881378588)，发现里面好像没有写怎么配置，所以自己琢磨弄了半天（没办法，我很菜），终于弄好了，所以记录在这里分享给大家。
首先，我先去github上把项目克隆到本地（需要JDK8或以上的版本，Tomcat版本至少是9），导入Eclipse中，并且把**mail.properties**进行如下的配置。

![](https://pan.layne666.cn/images/2021/12/02/PbDLZDGC50.png)

user是QQ邮箱，密码我一开始以为就是QQ密码 😂
其实并不是，是授权码。

现在，需要登录QQ邮箱，在设置—>账号中开启smtp服务，然后生成授权码，把授权码填入到mail.properties的password。

![](https://pan.layne666.cn/images/2021/12/02/yYTgp2ifNG.png)

![](https://pan.layne666.cn/images/2021/12/02/zzJ3zx8iMn.png)

我把这些配置完之后就开始跑项目了，发现邮件还是没发出去，控制台出现报错信息。

![](https://pan.layne666.cn/images/2021/12/02/y4p9lyERqk.png)

没办法，出现报错信息，只能调试看看了！别说，我还真发现点东西。

![](https://pan.layne666.cn/images/2021/12/02/rDkgbQDdUR.png)

![](https://pan.layne666.cn/images/2021/12/02/nYvlQyY2Pj.png)

![](https://pan.layne666.cn/images/2021/12/02/kuYjKhYATi.png)

好像是adminEmail和mail.properties里面的user邮箱设置的不一致，然后就会报这个错！
我的adminEmail里面的值是layne666@ solo.b3log.org，这应该是b3log给的默认邮箱，所以我寻思着能不能把这个改成我的QQ邮箱。

我查数据库发现，**表b3_solo_option**里面有这个值的设置，二话不说，改成我的QQ邮箱再说

![](https://pan.layne666.cn/images/2021/12/02/zPWaH3PyEE.png)

![](https://pan.layne666.cn/images/2021/12/02/AmllA4CjTA.png)


改完之后，重新跑一下项目。然后我回复评论，回复成功了，邮件也发出去了，小号成功收到邮件。

![](https://pan.layne666.cn/images/2021/12/02/W0Dn27amZZ.png)

到此算是暂告一段落了！

![](https://pan.layne666.cn/images/2021/12/02/KL55NrAbg2.gif)

讲道理，能看到[Solo](https://github.com/b3log/solo)的源码，真得很棒，很值得学习，感谢D大，感谢为Solo贡献的所有人！💖