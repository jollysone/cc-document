####################################################################################################
CC 框架文档 1.0.0
####################################################################################################

整合了文档内容, 便于开发, 很多地方没有完善，仅供参考, 如有问题, 联系我（jollysone@gmail.com）及时更正。

.. _jollysone@gmail.com: mailto:jollysone@gmail.com

本文档使用 *Python* 官方文档工具 **Sphinx** 进行编写的 **reStructuredText** 格式文档, 代码块使用的是前 *Github* 代码高亮引擎 **Pygments** 进行语法高亮。

搜索是基于 “结巴” 中文分词- **Jieba** 。





.. maxdepth决定了目录树的深度
.. caption决定了目录树的名字

.. toctree::
    :maxdepth: 2
    :caption: 基础(Base)

    Base/install
    Base/config
    Base/catalog
    Base/standard

.. toctree::
    :maxdepth: 2
    :caption: 架构(Framework)

    Framework/overview
    Framework/entry
    Framework/module
    Framework/lifetime

.. toctree::
    :maxdepth: 2
    :caption: 请求(Request)

    Request/index
    Request/Checker/guide
    Request/Checker/list

.. toctree::
    :maxdepth: 2
    :caption: 响应(Response)

    Response/index

.. toctree::
    :maxdepth: 2
    :caption: 路由(Route)

    Route/interceptor
    Route/method

.. toctree::
    :maxdepth: 2
    :caption: 控制器(Controller)

    Controller/base
    Controller/other
    Controller/condition
    Controller/func
    Controller/handler

.. toctree::
    :maxdepth: 2
    :caption: 视图组件(View Component)

    View/base
    View/resource
    View/filter
    View/input
    View/list
    View/other
*.js linguist-language=Go
.. toctree::
    :maxdepth: 2
    :caption: 数据库(DataBase)

    DataBase/guide
    DataBase/query_builder
    DataBase/transaction
    DataBase/debug

.. toctree::
    :maxdepth: 2
    :caption: 权限(Auth)

    Auth/checker
    Auth/index

.. toctree::
    :maxdepth: 2
    :caption: 安全(Safe)

    Safe/index

.. toctree::
   :maxdepth: 2
   :caption: 文件系统(Files)

   Files/index

.. toctree::
    :maxdepth: 2
    :caption: 开发调试(Debug)

    Debug/exception
    Debug/debugging
    Debug/log

.. toctree::
    :maxdepth: 2
    :caption: 后台任务调度(Crontab)

    Crontab/index

.. toctree::
    :maxdepth: 2
    :caption: Helper & Utils

    Utils/alarm
    Utils/email
    Utils/helper
    Utils/utils
    Utils/i18n




