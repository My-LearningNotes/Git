``git diff``
============

``git diff``\ 命令用于显示文件之间的修改.

``git diff``\ 可以用来查看不同域之间文件的修改:

    * 工作区和暂存区之间
    * 工作区和版本库中的commit之间
    * 暂存区和版本库中的commit之间
    * 版本库中的commit之间

``git diff``\ 可以用来查看指定文件或所有文件的修改:

    * 如果指定了文件, 则查看指定文件的修改;
    * 如果没有指定文件, 则查看所有文件的修改.


示例
----

* ``git diff <file> ...``

    没有显式指定比较的域, 表示在工作区和暂存区比较;

* ``git diff commit <file> ...``

    如果只指定了一个表示commit的参数, 表示在工作区和指定的commit之间比较.

    Example:

    .. code-block:: sh

        # 在当前工作区和版本库中当前commit之间比较指定的文件
        git diff HEAD file

* ``git diff --cached/--staged <file> ...``

    ``--cached/--stated``\ 表示在暂存区和版本库中当前commit之间比较;

* ``git diff <commit_id1> <commit_id2> <file> ...``

    在版本库中两个指定的commit之间比较;

* ``git diff <branch1> <branch2>``
    
    在指定的branch之间比较(实质是branch指针指向的commit之间).

* ``git diff --stat``

    仅仅比较统计信息.

