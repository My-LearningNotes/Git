``git mv``
==========

``git mv``\ 命令用于\ **移动**\ 或\ **重命名**\ 文件, 目录或符号链接.

``git mv <source> <destination>``

    * 如果\ ``<source>``\ 存在且\ ``<destination>``\ 不存在, 表示重命名;
    * 如果\ ``<source>``\ 存在且\ ``<destinaiton>``\ 是一个已存在的目录, 表示移动.


``mv``\ 和\ ``git mv``
----------------------

常规的\ ``mv``\ 命令也可以用来移动或重命名, 但在Git中使用\ ``git mv``\ 要更加快捷, 相当于将多个操作合而为一.

.. note::

    ``mv``\ 指令只是移动/重命名文件, 但是并没有将这个操作记录在Git中;
    ``git mv``\ 不但移动/重命名文件, 还将这个操作记录在Git中.


例如, 把一个文件\ *text.txt*\ 移动到\ *mydir*\ , 可以执行以下操作:

    .. code-block:: sh

        git mv test.txt mydir

如果使用\ ``mv``\ 指令, 就需要下面3条指令:

    .. code-block:: sh

        mv test.txt mydir
        git rm test.txt
        git add mydir

.. note::

    ``mv``\ 指令只是移动或重命名文件, 但是并没有将这个操作记录在Git中;
    而\ ``git mv``\ 不但移动/重命名文件, 还将这个操作记录在Git中.

