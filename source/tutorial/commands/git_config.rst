``git config``
==============

``git config``\ 命令用于对Git进行各种配置.

配置项的作用域和配置文件的存储位置
----------------------------------

配置项可以使用三个选项: ``--local``\ , ``--global``\ 和\ ``--system``\ , 分别对应三个不同的作用域.

    * ``--local``  - 项目作用域, 表示配置项只在Git项目中有效;
    * ``--global`` - 用户作用域, 表示配置项对当前用户的所有Git项目有效;
    * ``--system`` - 系统作用域，表示配置项对当前机器上的所有用户的所有Git项目有效.

如果不同作用域中有重复的配置项, 局部作用域覆盖全局作用域.

不同作用域的配置项对应不同路径的配置文件:

    * ``--local``\ 对应的配置文件为: ``.git/config``, 即git目录中的config文件;
    * ``--global``\ 对应的配置文件为: ``~/.gitconfig``;
    * ``--system``\ 对应的配置文件为: ``/etc/gitconfig``.

配置用户名和邮箱
----------------

当安装Git后首先要做的事情就是设置用户名和e-mail地址, 这很重要, 应为每次Git提交都会使用该信息, 该信息会被嵌入到\ ``commit``\ 中.

.. code-block:: sh

    git config --global user.name "sylar.liu"
    git config --global user.email "sylar_liu65@163.com"
 
* 这里使用了\ ``--global``\ 选项;
* 如果希望在一个特定的项目中使用不同的名称或e-mail地址, 可以在该项目中运行该命令而不要使用\ ``--global``\ 选项.

.. code-block:: sh

    git config user.name "sylar.liu"
    git config user.email "sylar_liu65@163.com" 


配置编辑器
----------

.. code-block:: sh

    git config --global core.editor vim


配置差异比较工具
----------------

.. code-block:: sh

    git config --global diff.tool meld


配置合并冲突解决工具
--------------------

.. code-block:: sh

    git config --global merge.tool meld


检查配置
--------

* 可以使用\ ``git config --list``\ 命令来列出Git所有的配置参数;

* 也可以使用\ ``git config {key}``\ 查看一个特定的关键字的值.

    .. code-block:: sh

        git config user.name

        git config user.email

添加/删除配置项
---------------

* **添加配置项**

    .. code-block:: sh

        git config [--local | --global | --system] --add section.key value

    * 配置项默认是添加在\ ``local``\ 配置中;
    * 注意\ ``--add``\ 后面的\ ``section``, ``key``, ``value``\ 一项都不能少, 否则添加失败.

    Example:

    .. code-block:: sh

        git config --site.name abc

* **删除配置项**

    .. code-block:: sh

        git config [--local | --global | --sytem] --unset section.key

    Example:

        .. code-block:: sh

            git config --local --unset site.name

获取帮助
--------

如果在使用Git时需要帮助, 有三种方法可以获得git命令的手册页(manpage)帮助信息:

    .. code-block:: sh

        git help <verb>
        git <verb> --help
        man git <verb>

例如, 想要查看有关\ ``git config``\ 如何使用, 可以使用以下命令:

    .. code-block:: sh

        git help config
        git config -h/--help
        man git config



