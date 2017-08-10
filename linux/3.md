###bash命令行与github的结合使用

##注意事项
>一定不能有仓库套仓库的情况

###命令行（命令行比较长的时候，按q退出）
```
git log //查看版本历史
git status //查看仓库状态
git diff //查看具体修改的内容
```

###设置ssh
```
1.ssh-keygen
2.cd .ssh //进入.ssh文件
3.atom . //使用atom编辑器打开.ssh
4.选择id_ras.pub公钥，将里面的内容粘贴到github当中

>以后clone的时候，选择ssh模式就可以
```

###基本的操作步骤
```
git clone ～ //会在本地创建这个与远端建立连接的文件夹
//在本地做好编译之后：
git add . || git add -A  //所有修改都添加到git
git commit -m 'name' //版本留言（描述本次操作灰做了些什么） 注：每次修改后都要生成一个新的版本
git push //上传（首次使用会弹出登录窗，可以制作ssh）
```

###本地代码如何传入git
```
git init //将本地的普通的文件夹变成git仓库->在github上创建与之同名的仓库（不要勾选README）
rm .git/ -rf //将init生成的.git隐藏文件删除
git add .
git commit -m 'name'
git remote add origin http://github.com/liulu1012/~.git //告知路径
git push -u origin master
```

###github分支更多了解
>在github中，只有liulu1012.github.io这个仓库可以部署静态网站，如果想别的仓库部署，则必须上传到该仓库的*gh-pages*这个分支上面
#关于分支的简单操作
```
git checkout //切换分支
git branch //查看处于哪个分支
git checkout -b gh-pages //创建并切换到gh-pages分支上
注：*push的时候应该指定的传到gh-pages分支上，即：
git push --set-upstream origin gh-pages
```
