``git rebase``
===============

``git rebase``\ 命令的作用是以另外一个分支为基础, 重建当前分支的父节点(将另一个分支的修改合并到当前分支).

基本语法:

    .. code-block:: sh

        # 以另外一个分支为基础, 重建当前分支的父节点
        git rebase <another_branch>
        

假设当前版本库的状况如下:

.. graphviz:: 

  digraph repo1{
   node[fillcolor=aquamarine, style=filled]
   rankdir = LR

   origin[label="origin", shape=box]
   c1[label="C1"]
   c2[label="C2"]
   mywork[label="mywork", shape=box]

   rankdir = LR

   origin -> c2
   c2 -> mywork [dir=back]
   c1 -> c2 [dir=back]

   {rank=same; origin, c2, mywork}
  }

假设我们在\ *mywork*\ 这个分支做了一些修改, 然后生成两个\ *commit*\; 与此同时, 其他人在\ *origin*\ 分支上做了一些修改并做了提交.
这意味着\ *origin*\ 和\ *mywork*\ 这两个分支各自\ *前进*\ 了.

现在的状况如下:

.. graphviz:: 

  digraph repo1{
   node [fillcolor=aquamarine, style=filled]
   rankdir = LR

   origin [label=origin, shape=box]
   mywork [label=mywork, shape=box]
   c1[label=C1]
   c2[label=C2]
   c3[label=C3]
   c4[label=C4]
   c5[label=C5]
   c6[label=C6]

   c1 -> c2 -> c3 -> c4 [dir=back]
   c2 -> c5 -> c6 [dir=back]
   origin -> c4
   c6 ->mywork [dir=back]

   {rank=same; c3, c5}
   {rank=same; origin, c4, c6, mywork}
  }

可以使用\ ``git pull``\ 命令把\ ``origin``\ 分支上的修改拉取下来并且和当前分支合并，生成一个新的\ *合并提交(merge commit)*\ .

.. code-block:: sh

    git checkout mywork
    git merge origin

.. graphviz::

    digraph repo3{
        label = "git merge"
        fontsize = 30
        fontcolor = lawngreen
        node [fillcolor=aquamarine, style=filled]
        rankdir = LR

        origin [label=origin, shape=box]
        mywork [label=mywork, shape=box]
        c1 [label=C1]
        c2 [label=C2]
        c3 [label=C3]
        c4 [label=C4]
        c5 [label=C5]
        c6 [label=C6]
        c7 [label=C7, color=red]

        c1 -> c2 -> c3 -> c4 [dir=back]
        c4 -> c7 [dir=back, color=red]
        c2 -> c5 -> c6 [dir=back]
        c6 -> c7 [dir=back, color=red]
        origin -> c4
        c7 -> mywork [dir=back]

        {rank=same; c3, c5}
        {rank=same; origin, c4, c6}
        {rank=same; c7, mywork}
      }

但是, 如果想让\ *mywork*\ 分支的历史看起来像没有经过任何合并一样, 可以使用\ ``rebase``.

.. code-block:: sh

    git checkout mywork
    git rebase origin

.. graphviz::

    digraph repo4{
        label = "git rabase"
        fontsize = 30
        fontcolor = lawngreen
        rankdir = LR
        node [fillcolor=aquamarine, style=filled]

        origin [label=origin, shape=box]
        mywork [label=mywork, shape=box]
        c1 [label=C1]
        c2 [label=C2]
        c3 [label=C3]
        c4 [label=C4]
        c5 [label=C5]
        c6 [label=C6]
        c7 [label="C5'", color=red]
        c8 [label="C6'", color=red]

        c1 -> c2 -> c3 -> c4 -> c7 -> c8
        origin -> c4
        c8 -> mywork [dir=back]
        c2 -> c5 -> c6

        {rank=same; origin, c4, c6}
        {rank=same; c8, mywork}
    }


rebase的过程
------------

*rebase*\ 并不是简单的剪下/贴上commits的过程, 在\ *rebase*\ 过程中会生成commits, 并重新计算commits的Id.

.. graphviz::

    digraph repo5{
        rankdir = LR

       c1 [label="e12d8e", fillcolor=red, style=filled]
       c2 [label="b69eb6", fillcolor=red, style=filled]
       c3 [label="053fb2", fillcolor=red, style=filled]
       c4 [label="35bc86", fillcolor=red, style=filled]
       c5 [label="28a76d", fillcolor=red, style=filled]
       
       c6 [label="c68537", fillcolor=azure4, style=filled]
       c7 [label="b174a5", fillcolor=azure4, style=filled]

       cur_head [label=HEAD, fillcolor=blue,  style=filled, shape=box]
       cur_cat [label=cat, fillcolor=green, style=filled, shape=box]
       dog [label=dog, fillcolor=green, style=filled, shape=box]
       master [label=master, fillcolor=green, style=filled, shape=box]
   
       prev_head [label=HEAD, fillcolor=azure4, style=filled, shape=box]
       prev_cat [label=cat, fillcolor=azure4, style=filled, shape=box]

       c1 -> c2 -> c3 -> c4 -> c5 [dir=back]
       c1 -> c6 -> c7 [dir=back, color=azure4]
       master -> c1
       dog -> c3
       cur_head -> cur_cat -> c5
       prev_head -> prev_cat -> c7

       {rank=same; master, c1}
       {rank=same; dog, c3, c7, prev_cat, prev_head}
       {rank=same; cur_head, cur_cat, c5}
       {rank=same; c7, prev_cat, prev_head}
    }

以上面的例子来说, \ *rebase*\ 的过程大致如下:

    * 先将\ ``c68537``\ 这个commit接到\ ``053fb2``\ 这个commit上, 因为\ ``c68537``\ 原本的上一层commit是\ ``e12d8e``\, 现在要接到\ ``053fb2``\ 上, 
      所以要重新计算这个commit的SHA-1值, 重新生成一个新的commit对象\ ``35bc96``\ ;
    * 再将\ ``b174a5``\ 这个commit接到刚才那个新生成的commit对象\ ``35bc96``\ 上, 同理, 因为\ ``b174a5``\ 这个commit要接到新的commit的原因, 
      所以它也会重新计算SHA-1值, 得到一个新的commit对象\ ``28a76d``\ ;
    * 最后, 原本的分支指针\ ``cat``\ 是指向\ ``b174a5``\ 这个commit, 现在要改为指向那个新的commit对象\ ``28a76d``\ ;
    * ``HEAD``\ 还是指向\ ``cat``\ 分支.


谁rebase谁有差吗?
-----------------

以最后的档案来说没什么差别, 但以历史记录来说有差别, 谁rebase谁, 会造成历史记录上的先后顺序的不同.


rebase时出现冲突
----------------

在\ *rebase* \的过程中, 也许会出现冲突(*conflict*).
在这种情况下, Git会停止\ *rebase*\ 并提示解决冲突; 在解决完冲突后, 使用\ ``git add``\ 命令更新这些内容到暂存区, 
然后执行\ ``git rebase --continue``\ , 这样Git会继续应用余下的补丁.

或者, 当\ *rebase*\ 出现冲突时, 可以使用\ ``git rebase --abort``\ 命令来终止\ *rebase*\ 的操作, 并使分支回到\ *rebase*\ 之前的状态.


取消rebase
----------

使用\ ``git merge``\ 进行的合并, 通常使用\ ``git reset --hard HEAD^``\ 就可以回退到合并之前的状态.
对于\ ``git rebase``\, ``git reset --hard HEAD^``\ 只会回退到前一个commit, 并不会回到rebase之前的状态.

* 使用\ ``git reflog``

    使用\ ``git reflog``\ 查看rebase之前的\ *commit id*\ , 然后使用\ ``git reset --hard commit_id``\ 退回到rebase之前的状态.

* 使用\ ``ORIG_HEAD``

    在Git中有一个特别的记录点叫\ ``ORIG_HEAD``\ , 会记录\ **危险操作**\ 之前\ ``HEAD``\ 的位置.
    例如分支合并或是reset之类的都算是所谓的危险操作.

    透过这个记录点来取消\ ``git rebase``\ 相对的简单: ``git reset --hard ORIG_HEAD``\ .


何时使用\ ``git rebase``\
-------------------------

使用\ ``git rebase``\ 来合并的好处是它不像\ ``git merge``\ 那样生成一个额外的\ **合并提交**\, 而且历史顺序可以按照谁rebase谁而决定;
但缺点就是它相对的比一般的合并来得没那么直觉, 而且不小心可能会弄坏掉而且不知道怎么reset回来, 或是发生冲突的时候就会停在一半, 对不熟悉\ ``git rebase``\ 的人来说是个困扰.

通常还没有推送(``push``)出去但感觉有点乱的commit，可以使用\ ``git rebase``\ 整理再推送出去.
但\ ``git rebase``\ 等于是修改历史, 修改已经推送出去给别人的历史可能会对他人造成困扰, 所以对于已经推送出去的内容, 非必要的话应该尽量避免使用\ ``git rebase``\ .


******

参考文章:

    `另一种合并方式(使用rebase) <https://gitbook.tw/chapters/branch/merge-with-rebase.html>`_
