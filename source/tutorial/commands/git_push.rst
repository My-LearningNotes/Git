``git push``
============

``git push``\ 命令用于将本地分支的修改, 推送到远程仓库的分支上.
推送分支时, 会将本地分支的历史记录一同推送过去, 但和远程分支合并时\ **合并的只是分支头**\ .

基本语法为:

    .. code-block:: sh

        git push <remote_repo> <local_branch>:<remote_branch>

* 如果对应的\ ``<remote_branch>``\ 在远程仓库中不存在, 则在远程仓库中创建该远程分支;

* ``:<remote_branch>``\ - 推送一个空的本地分支到远程分支, 表示在远程仓库中删除指定的远程分支;

    ``git push <remote_repo> :<remote_branch>``\ 相当于\ ``git push <remote_repo> --delete <remote_branch>``.

* ``git push <remote_repo> <local_branch>``

    省略\ ``<remote_branch>``\ 表示将\ ``<local_branch>``\ 推送到同名的远程分支上, 如果对应的远程分支不存在, 则在远程仓库中创建该远程分支.

* 如果当前分支是某个远程分支的追踪分支, 可以直接使用\ ``git push``

    .. code-block:: sh
 
        # 将当前分支推送到远程追踪分支
        git push

* ``git push -u``

    可以在使用\ ``git push``\ 命令时使用\ ``-u``\ 选项, 表示将推送的远程分支设置为\ ``upstream``\ , 
    这样在以后推送时, 直接使用\ ``git push``\ 即可.


.. note::

    不带任何参数的\ ``git push``\ , 默认只推送当前分支, 这叫做\ ``simple``\ 方式.
    此外, 还有一种\ ``matching``\ 方式, 会推送所有有对应的远程分支的本地分支.
    Git 2.0版本之前, 默认采用\ ``matching``\ 方式, 现在改为默认采用\ ``simple``\ 方式.
    如果要修改这个设置, 可以使用\ ``git config``\ 命令.

    .. code-block:: sh

        git config --global push.default matching
        # 或
        git config --global push.default simple


* 推送标签到远程仓库/删除标签

    默认情况下, ``git push``\ 不会推送标签.

    * 推送所有标签

    .. code-block:: sh

        # 使用--tags选项推送所有标签
        git push <remote_repo> --tags

    * 推送指定标签

    .. code-block:: sh

        # 通过指定标签名, 推送指定的标签
        git push <remote_repo> tag_name

    * 删除标签
        
    .. code-block:: sh

        # 删除标签的方式类似于删除远程分支
        git push <remote_repo> :tag_name
        # 或
        git posh <remote_repo> --delete tag_name

* 重命名远程分支名

      * 删除旧的分支
      * 推送时创建一个新的分支

