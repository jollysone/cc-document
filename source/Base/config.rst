####################################################################################################
**配置**
####################################################################################################

******************************************************************************************
**配置文件列表**
******************************************************************************************

一共有 ``三个配置文件`` ，对应每个服务器的对应配置文件，内容相同，具体服务器特殊需要可增加相关配置。

.. code-block:: 

    project/conf_deve.php   // 开发服配置文件
    project/conf_test.php   // 测试服配置文件
    project/conf_zhengshi.php   // 正式服配置文件

******************************************************************************************
**配置文件内容**
******************************************************************************************

================================================================================
**配置文件详情**
================================================================================

配置文件内容只需要了解 ``数据库配置`` 即可。

.. code-block:: php
    :linenos:
    :emphasize-lines: 3-7

    <?php
        return array(
            'db' => array(
                'dsn' => 'mysql:host=127.0.0.1;dbname=zf_deve_api',
                'username' => 'zf_deve',
                'password' => '',
            ),
            'env' => array(
                'debug' => true,
                'language' => 'zh_cn',
                'alioss' => array(
                    'open' => true,
                    'pre_dir' => 'xbqw',
                    'bucket' => 'xbwq',
                    'endpoint' => 'oss.aliyuncs.com'
                ),
            ),
            'params' => array(
                'is_debug_other_server' => TRUE,

                'baidu_ak' => 'DcgF6ydVi9CdfetYB6GjHNVOEsGnLVsX',
                'baidu_service_id' => '213544',
                'baidu_yingyan_limit_url' => 'http://114.55.174.180:8086/api/loc/upload/yinyan',

                'mock_digit_city' => true,

                //zf_deve_zf_yg  程序里面会自己加 _yg
                'autocomplete_url' => 'http://127.0.0.1:9400/zf_deve_zf',
                'template_com_id' => 6048,
                'imgurl' => 'http://xbwq.oss.aliyuncs.com',
                'qw_wx_url' => 'http://qinwuwx-test.xbwq.com.cn/qinwuwx/qwapp',
                'cc_debug' => true,
                'env_is_dev' => true,

                'im_url' => 'http://127.0.0.1:6282/plugins/userservice',
                'interface_url' => 'http://zf.zfdeve.xbcx.com.cn/wqinterface',
                'xz_url' => 'http://zf.zfdeve.xbcx.com.cn/xz',

                'title_show_ver' => true,
                'no_copy_page' => true,

                'sdkAppId_live' => '1400019851',  //视频回传 腾讯云appID
                'accountType_live' => '9300',     //视频回传 腾讯云accountType
                'sdkAppId_talk' => '1400019855',  //对讲 腾讯云appID
                'accountType_talk' => '9039',     //对讲 腾讯云accountType
                'qcloud_type' => 't',  //服务器类型 t=勤务测试服 f=勤务正式服 o=勤务海外服 fhj=访惠聚
                'redis_conf' => array(
                    'connect' => array(
                        array(
                            'host' => '10.132.34.136',
                            'port' => 11766,
                            'password' => 'dz6w47PJYLby5KPQ',
                        )
                    ),
                    'key_pre' => 'zf:'
                ),
                'dsj_grid_code_com_id' => [7012],
                'doc_to_html' => 'http://127.0.0.1:7070',
                'signit_conf' => [  //快捷签署配置
                    'appid' => '16923ac9f2f5e899b9f41309f71',
                    'secret' => 'sk962b42d0b58db90974ae70a4423bd89c',
        //            'token_url' => 'https://open.signit.cn/v1/oauth/oauth/token',
                    'token_url' => 'http://112.44.251.136:2576/v1/oauth/oauth/token',
                    'quick_sign_url' => 'http://112.44.251.136:2576/v1/open/signatures/quick-sign'
                ]
            )
        );

    ?>

================================================================================
**配置文件解读**
================================================================================

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
**自定义参数**
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: php
    :linenos:

    // 配置自定义参数 'test'
    <?php
        return array(
            ...

            'params' => [
                'test' => 1
            ],

            ...
        )
    ?>

.. code-block:: php
    :linenos:

    // 读取自定义参数 'test'
    <?php
        $test = \CC::app()->params['test'];
    ?>
   


^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
**数据库连接**
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: php
    :linenos:

    <?php
        return array(
            ...

            'db' => [
                'dsn' => 'mysql:host=192.168.1.1;port=3306;dbname=test',
                'username' => 'root',
                'password' => '123456',
            ],

            ...
        )
    ?>

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
**配置Redis连接**
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: php
    :linenos:

    <?php
        return array(
            ...

            'params' => [
                'redis_conf' => [
                    'connect' => [
                        'host' => '主机',
                        'password' => '密码',
                        'port' => '端口',
                        'timeout' => '超时时间(浮点数)',
                    ],
                    'key_pre' => '键前缀'
                ],

                ...

            ],

            ...
        )
    ?>

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
**加密盐**
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: php
    :linenos:

    <?php
        return array(
            ...

            'cc_class_config' => [
                'util/encrypt/Password' => [
                    'salt' => 'H6ku3dBNBxmSZmw7WMRT8fu4ce95mdda',
                ]
            ],

            ...
        )
    ?>

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
**分组默认布局文件**
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: php
    :linenos:

    <?php
        return array(
            ...

            'cc_class_config' => [
                'response/CRenderData' => [
                    'groupLayouts' => [
                        'admin' => '/layouts/default',
                        'web' => '/layouts/simple',
                        'api' => '/layouts/mobile',
                        'xbwqLink' => '/layouts/simple',
                    ],
                ],
            ],

            ...
        )
    ?>

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
**分组配置**
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: php
    :linenos:

    <?php
        return array(
            ...

            'env' => [
                'api' => 'api',
                'web' => 'admin,web',
                'cmd' => 'cmd',
            ],

            ...
        )
    ?>
