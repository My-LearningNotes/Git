``git status``
==============

``git status``\ 命令用于显示工作区和暂存区的状态.
使用此命令能看到哪些修改被添加到了暂存区, 哪些没有, 哪些文件没有被Git track.

``git status``\ 不显示已经\ ``commit``\ 到项目中去的信息.
看项目历史的信息要使用\ ``git log``\ .


Untracked文件
-------------

untracked文件分为两类:

    * 已经放在工作区但是还没有执行\ ``git add``\ 的;
    * 在\ ``.gitignore``\ 中定义的要忽略的文件.
