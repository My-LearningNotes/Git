``git reset``
=============

``git reset``\ 命令用于将当前\ ``HEAD``\ 复位到指定状态或用指定commit中的文件快照恢复暂存区中的文件.
一般用于撤销之前的一些操作, 如\ ``git add``\ , ``git commit``\ 等.

.. note::

    下面这一段是一个牛人的解释: 
    
        总的来说, ``git reset``\ 命令是用来将当前\ *branch*\ 重置到另外一个\ *commit*\ 的, 而这个动作可能会将\ *index*\ 以及\ *work tree*\ 同样影响.

相关的基本概念
--------------

先来看几个基本的概念:

* ``HEAD``
    一个特殊的分支指针, 指向某一个分支, 表示当前分支(或者说当前\ *commit*\);
    ``HEAD``\ 可以在不同的分支的不同\ *commit*\ 之间切换.

* ``分支``
    一个分支其实就是一个指针, 指向一个commit;
    分支指针可以在该分支的历史中移动, 指向不同的commit(分支指针只能指向固定的一个分支).

* ``Index``
    ``index``\ 也被称为\ ``staging area``, 是指一整套即将被下一个提交的文件集合.

* ``Working Copy``
    表示正在工作的那个文件集.


重置\ ``HEAD``\ 和分支指针到指定的状态
--------------------------------------

.. code-block:: sh

    # 将HEAD和branch重置到指定的commit状态
    git reset [<commit>]

需要注意, ``git reset``\ 和\ ``git checkout``\ 是不一样的:

    * ``git checkout``\ 只改变\ ``HEAD``\ 的指向, 使其指向不同的\ *branch*\ ;
    * ``git reset``\ 使\ ``HEAD``\ 重置到某个\ *commit*\ 的状态, 同时使分支指针也重置到该\ *commit*\ 状态.


假设有如下的\ ``master``\ 分支, 图形化表示如下:

.. graphviz::

    digraph abc{

        master[shape=plaintext];
        HEAD[shape=plaintext];
        a349c9[style=filled];
        f9ad39[style=filled];
        ae9e88[style=filled];
        f38f33[style=filled];


        {rank = same; master -> a349c9};
        {rank = same; a349c9 -> HEAD[dir=back]};

        a349c9 -> f9ad39 -> ae9e88 -> f38f33[style=filled];
    }

开始时, \ ``master``\ 和\ ``HEAD``\ 都指向\ ID为\ ``a349c9``\ 的\ *commit*\ .


如果我们执行:

.. code-block:: sh

    git reset HEAD

什么事都不会发生, 这是因为我们告诉git重置这个分支到\ ``HEAD``\ 指向的\ *commit*\ , 而这个正是它现在所在的位置.

.. code-block:: sh

    git reset HEAD~1

上面的命令表示将当前分支\ ``master``\ 和\ ``HEAD``\ 重置到\ ``HEAD``\ 之前的那个\ *commit*\ , 即\ ``f9ad39``\ .

.. note::

    ``HEAD``\  表示当前指向的那个\ *commit*\ ;

    ``HEAD~1``\ 或\ ``HEAD^``\ 表示当前指向的那个\ *commit*\ 的前一个\ *commit*\ ;

    ``HEAD~2``\ 或\ ``HEAD^^``\ 表示当前指向的那个\  commit*\ 的前一个\ *commit*\ 的前一个\ *commit*\ ;

    ``HEAD~N``\ 一次类推.


.. graphviz::
    
    digraph abc{

        master[shape=plaintext];
        HEAD[shape=plaintext];
        a349c9[style=filled];
        f9ad39[style=filled];
        ae9e88[style=filled];
        f38f33[style=filled];


        {rank = same; master -> f9ad39};
        {rank = same; f9ad39 -> HEAD[dir=back]};

        a349c9 -> f9ad39 -> ae9e88 -> f38f33[style=filled];
    }


参数
----

* ``--soft``

    ``--soft``\ 参数表示将\ ``HEAD``\ 和\ ``branch``\  重置到指定的\ *commit*\ , 但是\ ``index``\ 和\ ``working copy``\ 都不会有任何变化, 所有的\ ``original HEAD``\ 和重置到的那个
    \ *commit*\ 之间的所有差异都放在\ ``stage(index)``\ 区域中.

* ``--hard``

    ``--hard``\ 参数会将\ ``HEAD``\ 和\ ``branch``\ 重置到指定的\ *commit*\ , 同时\ ``index``\ 和\ ``working copy``\ 也会重置到一样的状态.
    这是一个比较危险的动作, 具有破坏性, 数据因此可能会丢失.

    如果我们希望丢掉\ ``working copy``\ 和\ ``index``\ 中的修改而又不希望更改\ ``HEAD``\ 和\ ``branch``\ 所指向的\ *commit*\ , 可以执行:

    .. code-block:: sh
        
        git reset --hard HEAD

    或

    .. code-block:: sh

        git reset --hard

    另一个使用场景是简单地移动\ ``branch``\ 从一个到另一个\ ``commit``\ , 同时保持\ ``index/working area``\ 的同步.

* ``--mixed(default)``

    ``--mixed``\ 是\ ``reset``\ 的默认参数, 也就是当不指定任何参数时的参数.
    它将重置\ ``HEAD``\ 和\ ``branch``\ 到指定的\ *commit*\ , 并且重置\ ``index``\ 但是不会更改\ ``working copy``\ .

    所有该\ ``branch``\ 上从\ ``original HEAD``\ 到重置到的那个commit之间的所有修改, 以及暂存区相对工作区之间的修改，
    都将作为\ *local modifications*\ 保存在\ *working area*\ 中(被标示为local modification or untracked via ``git status``), 
    但是并未staged的状态, 可以重新检视然后再修改和提交.


``git reset``\ 和\ ``git checkout``\ 的区别
-------------------------------------------

``git reset``\ 是将\ ``HEAD``\ 和\ ``branch``\ 重置到指定的\ ``commit``\, 根据参数的不同, 还可能重置\ ``index``\ 和\ ``working copy``\ .

``git checkout``\ 是切换\ ``HEAD``\ 指向指定的\ ``commit``\ , 


用指定\ ``commit``\ 中的文件快照恢复暂存区中的文件状态
------------------------------------------------------

.. code-block:: sh

    git reset commit <file> ...

