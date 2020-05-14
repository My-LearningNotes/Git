``git branch``
===============

``git branch``\ 命令用于\ **列出**\ , \ **创建**\ 或\ **删除**\ 分支.

* 列出分支 - ``git branch``\ 或\ ``git branch --list``

    列出现有的分支, 当前分支将以星号突出显示.

    * ``-r`` - 列出远程跟踪分支;
    * ``-a`` - 列出所有分支(本地和远程分支).

* 创建新的分支 - ``git branch <branch-name> [<start-point>]``

    从指定的\ ``commit``\ 创建一个新的分支, 如果没有指定\ ``start-point``\ , 则从当前\ ``HEAD``\ 指向的\ ``commit``\ 创建新的分支
    (注意: 只是创建新的分支而没有切换过去).
    
* 分支重命名 - ``git branch -m <old-branch-name> <new-branch-name>``

* 删除分支 - ``git branch -d <branch-name>``\ 或\ ``git branch -D <branch>``

    * 不能删除当前所在的分支;
    * 通常, 删除一个分支使用\ ``-d``\ 选项就可以了, 但是如果要删除一个没有被合并过的分支, 需要使用\ ``-D``\ 选项.

