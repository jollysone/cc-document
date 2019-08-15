####################################################################################################
**开发规范**
####################################################################################################

******************************************************************************************
PHP开发规范
******************************************************************************************

- **PSR-1： 基本编码标准** （Basic-Coding-Standard_）

.. _Basic-Coding-Standard: https://www.php-fig.org/psr/psr-1/


- **PSR-2： 编码风格指南** （Coding-Style-Guide_）

.. _Coding-Style-Guide: https://www.php-fig.org/psr/psr-2/


- **PSR-3： 日志记录器接口** （Logger-Interface_）

.. _Logger-Interface: https://www.php-fig.org/psr/psr-3/


- **PSR-4： 自动加载器** （Autoloader_）

.. _Autoloader: https://www.php-fig.org/psr/psr-4/


- **PSR-6： 缓存接口** （Caching-Interface_）

.. _Caching-Interface: https://www.php-fig.org/psr/psr-6/


- **PSR-7： HTTP消息接口** （HTTP-message-interfaces_）

.. _HTTP-message-interfaces: https://www.php-fig.org/psr/psr-7/


- **PSR-11：容器接口** （Container-interface_）

.. _Container-interface: https://www.php-fig.org/psr/psr-11/


- **PSR-13：链路定义接口** （Link-definition-interfaces_）

.. _Link-definition-interfaces: https://www.php-fig.org/psr/psr-11/


- **PSR-14：事件调度程序** （Event-Dispatcher_）

.. _Event-Dispatcher: https://www.php-fig.org/psr/psr-14/


- **PSR-15：HTTP服务器请求处理程序** （HTTP-Server-Request-Handlers_）

.. _HTTP-Server-Request-Handlers: https://www.php-fig.org/psr/psr-15/


- **PSR-16：缓存库的通用接口** （Common-Interface-for-Caching-Libraries_）

.. _Common-Interface-for-Caching-Libraries: https://www.php-fig.org/psr/psr-16/


- **PSR-17：HTTP工厂** （HTTP-Factories_）

.. _HTTP-Factories: https://www.php-fig.org/psr/psr-17/


- **PSR-18：HTTP客户端** （HTTP-Client_）

.. _HTTP-Client: https://www.php-fig.org/psr/psr-18/

- **...**




******************************************************************************************
存储规范
******************************************************************************************

.. code-block:: 

    app/protected/module/    各模块的相关文件都必须存储在这个路径

******************************************************************************************
命名规范
******************************************************************************************

**文件及目录定义方式**

**路由访问默认方式：** ``.../分组/模块/子模块/控制器名`` ,  ``定义路由后可自定义使用路由访问方式``。

**样例：** ``http://domain/root/group/module/controller/actionName``。 不写模块名两者都能访问。

========== ===========================  ======================================================
 **分组**         **路由**                            **访问文件**
---------- ---------------------------  ------------------------------------------------------
   admin     /admin/file/manage/list       /module/file/manage/FileManageListAdminAction.php
---------- ---------------------------  ------------------------------------------------------
    api      /admin/file/manage/list       /module/file/manage/FileManageListApiAction.php
========== ===========================  ======================================================


.. code-block:: 

    ├─module        应用模块
    │  ├─file          文件模块
    │  │  ├─manage    子模块
    │  │  │    ├─...
    │  │  │    └─FileManageListAction.php
    │  │  └─...
    │  └─...

**变量命名方式**

请勿使用没有意义的变量进行命名, 使用英文翻译尽量达意。

.. code-block:: php
    :linenos:

    // 测试路径日志变量
    <?php
        // error
        $cs = 'ceshi';
        $ceshi = 'ceshi';
        $a1 = 'ceshi';

        // correct
        $test_trace_log = 'ceshi';
        $testTraceLog = 'foo';
    ?>

******************************************************************************************
其他规范
******************************************************************************************

================================================================================
1. 等号两侧使用空格隔开
================================================================================

.. code-block:: php
    :linenos:

    <?php

        // error
        $test_trace_log='ceshi';
        $test_operate_log ='ceshi';
        $test_user_log= 'ceshi';

        // correct
        $correct_arg_standard = 'foo';

    ?>

================================================================================
2. 尽可能的使用别名
================================================================================

.. code-block:: php
    :linenos:
    :emphasize-lines: 10

    <?php

        // error
        ItemModel::make('user')
            ->select('phone')
            ->execute();

        // correct
        ItemModel::make('user')
            ->select('t.phone')
            ->execute();

    ?>

================================================================================
3. 合理的缩进
================================================================================

.. code-block:: php
    :linenos:
    :emphasize-lines: 5-8,12-16

    <?php

        // error
        ItemModel::make('user')
        ->rightJoin('logs', 'l', 't.id = l.uid and t.phone = ? and l.time = ?', [
            '13011118899',
            '2019-08-08 12:34:56'])
        ->execute();

        // correct
        ItemModel::make('user')
            ->rightJoin('logs', 'l', 't.id = l.uid and t.phone = ? and l.time = ?', [
                '13011118899',
                '2019-08-08 12:34:56'
            ])
            ->execute();

    ?>


.. code-block:: php
    :linenos:

    <?php

        // error
        protected function getPostNames()
        {
            return "happen_time,handle_time,operate_time,create_time,end_time,address,lng,lat,case_type,case_source,case_attribute,main_sponsor,co_sponsor";
        }

        // correct
        protected function getPostNames()
        {
            return "happen_time,handle_time,operate_time,create_time,end_time
                    address,lng,lat,
                    case_type,case_source,case_attribute,
                    main_sponsor,co_sponsor";
        }

    ?>

================================================================================
4. 使用全局宏/枚举值
================================================================================

.. code-block:: php
    :linenos:

    <?php

        // error
        ItemModel::make('user')->execute();

        // correct
        ItemModel::make(\DBUtils::USER)->execute();

    ?>


.. code-block:: php
    :linenos:
    :emphasize-lines: 5,8,11,21,24,27

    <?php

        // error
        switch ($data['sub_status']){
                case 1:
                    $msg = '待查看';
                    break;
                case 2:
                    $msg = '待处理';
                    break;
                case 3:
                    $msg = '处理中';
                    break;
                default:
                    $msg = '未知状态';
                    break;
        }

        // correct
        switch ($data['sub_status']){
                case TaskOpTypeEnum::WAIT_LOOK:
                    $msg = '待查看';
                    break;
                case TaskOpTypeEnum::WAIT_HANDLE:
                    $msg = '待处理';
                    break;
                case TaskOpTypeEnum::HANDLING:
                    $msg = '处理中';
                    break;
                default:
                    $msg = '未知状态';
                    break;
        }

    ?>



