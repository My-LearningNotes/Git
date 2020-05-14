``git log``
===========

``git log``\ 命令用于显示提交日志信息.

``git log``\ 有很多的选项, 可以控制显示的日志信息, 以下是一些示例:

* ``git log --no-merges``

    显示整个提交历史记录, 但跳过合并.

* ``git log -N``

    显示最近N次提交.

* ``git log --pretty=oneline``

    按指定格式显示日志信息, 可选项有: ``oneline``, ``short``, ``medium``, ``full``, ``fuller``, ``email``, ``raw``\ 以及\ ``format``;
    默认为\ ``medium``\ .

