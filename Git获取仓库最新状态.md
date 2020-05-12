##### Git获取仓库最新状态

> 适用于本地仓库没有,而github上面多了某个文件,背景是此时的master为目标master
>
> - clone之后进入最新创建的文件夹会自动调整为master状态

:pen: Git remote show origin 

> 展示当前的origin是什么,确定当前的pull拉下来的repo为目的仓库即可进行repo pull

:pen: git pull origin master 将最新状态的repo拉下来

---

##### 删除某个文件夹

只能是先clone下来或者已经在其本身仓库

:pen: git rm -f name[加r是递归删除name里面的所有文件，防止他是空的状态]

:pen: git commit -m "change"

:pen: git push origin master 将已经弄完的更新上去

:o: 最后git status 查看是否clean

 

