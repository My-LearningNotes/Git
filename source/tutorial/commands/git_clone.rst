``git clone``
==============

``git clone``\ 命令用来克隆Git版本库.

基本语法:

.. code-block:: sh
    :emphasize-lines: 1

    git clone <repo> [<dir>]

* 如果没有指定不同的目录, 则会在本地生成一个与远程版本库同名的目录;

* ``git clone``\ 会自动将克隆的仓库设置为\ ``tracked repository``\ 并默认命名为\ ``origin``;
  同时还会在本地版本库自动创建一个\ ``master``\ 分支, 并追踪\ ``origin/master``\ 分支;

* ``git clone``\ 支持多种协议, 除了HTTP(s)意外, 还支持SSH, Git, 本地文件协议等.

