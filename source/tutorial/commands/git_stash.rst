``git stash``
=============

``git stash``\ 命令用于将当前工作区和暂存区中的修改保存在一个\ *栈*\ 结构中, 从而保持当前工作目录的clean(工作区和暂存区的状态和\ ``HEAD``\ 一致).


* ``git stash list``
    
    列出所有储藏的修改, 以\ ``stash@{0}``, ``stash@{1}``, ...的形式列出.

* ``git stash show stash@{N}``

    显示指定的储藏的修改的信息, 如果没有指定则显示最近一次的信息.

* ``git stash/ git stash save``

    调用没有任何参数的\ ``git stash``\ 相当于\ ``git stash save``, 表示储藏当前的修改.
    默认情况下, 储藏列表为"分支名称上的WIP", 但您可以在创建一个消息时在命令行上给出更具描述性的消息, ``git stash save [<message>]``.

* ``git stash apply stash@{N}``

    * 应用编号为\ ``N``\ 的stash(即取回编号为N的修改), 应用之后该stash仍然保存在栈中;
    * ``git stash apply``\ 表示应用最近一次的stash;
    * 默认情况下, 应用stash时, 保存的被暂存的文件没有重新被暂存, 想那样的话, 可以加上\ ``--index``\ 选项: ``git stash apply --index``.

* ``git stash drop stash@{N}``

    移除指定的stash.

* ``git stash pop``

    从栈中弹出最近一次的stash, 该stash会从栈中移除.

* 取消储藏

    在某些情况下, 可能想应用储藏的修改, 在进行了一些其他的修改之后, 又要取消之前所应用储藏的修改.
    Git没有提供类似于\ ``stash unapply``\ 的命令, 但是可以通过取消该储藏的补丁达到同样的效果:

    .. code-block:: sh

        git stash show -p stash@{N} | git apply -R
 
* 从储藏中创建分支

    如果储藏了一些工作, 暂时不去理会, 然后继续在你储藏工作的分支上工作, 在重新应用工作时可能会碰到一些问题.
    如果尝试应用的变更是针对一个在那之后修改过的文件, 会碰到一个归并冲突并且必须去解决它.
    如果想用更方便的方法来重新校验储藏的变更, 可以运行\ ``git stash branch``\ , 这回创建一个新的分支, 检出储藏工作时的所处的提交, 重新应用工作, 如果成功，将会丢弃储藏.

