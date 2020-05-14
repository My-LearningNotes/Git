``git mergetool``
=================

``git mergetool``\ 命令用于运行合并工具来解决合并冲突, 通常在执行合并操作有冲突后运行.

* 如果给出一个或多个\ ``<file>``\ 参数, 则将运行合并工具程序来解决指定文件的差异(跳过那些没有冲突的文件);
* 指定目录将包括该路径中的所有未解析的文件;
* 如果没有指定\ ``<file>``\ 名称, ``git mergetool``\ 将在具有合并冲突的每个文件上运行合并工具程序.


设置\ ``git mergetool``\ 使用的可视化工具
-----------------------------------------

可以设置\ ``BeyondCompare``\ , \ ``DiffMerge``, \ ``meld``\ 等作为git的比较和合并的可视化工具, 方便操作.

设置如下:

    * 先安装工具, 这里以\ ``meld``\ 为例.

        .. code-block:: sh

            sudo apt-get install meld

    * 设置\ ``meld``\ 作为合并工具.

        .. code-block:: sh

            # mergetool配置
            git config --global merge.tool meld

使用方法如下:

    .. code-block:: sh

        git mergetool

