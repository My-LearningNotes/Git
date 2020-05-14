``git_fetch``
==============

``git fetch``\ 命令用于从另一个版本库中获取分支\ *和/或*\ 标签(统称为\ *引用*), 以及重现其历史所必须的对象.

默认情况下, 会获取指向历史记录的所有标签, 可以使用\ ``--tags``\ 或\ ``--no-tags``\ 选项来改变此默认行为.

.. note::

    使用\ ``git fetch``\ 获取分支, 并不是只获取当前的commit, 而是会将当前分支的历史一同获取.

基本语法:

    .. code-block:: sh

        # <repo>可以以shortname或URL的形式给出
        git fetch <repo> <branch>/<tag>

* ``FETCH_HEAD``\ 表示最近一次通过\ ``git fetch``\ 取回的分支;

    .. code-block:: sh

        git log FETCH_HEAD

* ``git fetch <repo>``

    .. code-block:: sh

        # 省略<branch>, 表示取回指定远程仓库上的所有分支
        # 从ref/heads/命名空间复制所有分支, 将它们保存在本地的refs/remotes/<repo>命名空间中
        git fetch <repo>
  
* ``git fetch``

    .. code-block:: sh

        # 省略<repo>, 默认表示取回origin上的所有分支
        git fetch

* 取回的远程分支存放在命名空间\ ``.git/refs/remotes/<repo>``\ 下;

    使用\ ``git branch -a/-r``\ 时, 在\ ``remotes``\ 命名空间下的分支表示远程分支.

    .. image:: images/remote_branches.png
 
* 将远程分支取回本地后, 可以像本地分支一样操作.

    * 从远程分支创建一个新的分支;

      .. code-block:: sh

          git checkout -b newBranch origin/master

    * 可以使用\ ``git merge``\ 或\ ``git rebase``\ 命令, 在本地分支上合并远程分支.

      .. code-block:: sh

          git merge origin/master
          # 或
          git rebase origin/master

