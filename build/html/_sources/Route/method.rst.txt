####################################################################################################
**路由使用方法(Route Guide)**
####################################################################################################

**路由文件：** protected/data/url.php

**路由规则：** '新路由路径' => '原路径地址'

.. Tip:: 只需要在 ``$urlMapping`` 中补充相应规则的路由即可。

.. code-block:: php
    :linenos:
    :emphasize-lines: 9

    <?php

        function _handl_url()
        {
            $urlMapping = array (
                '/alarm/getconfig' => '/alarm/index/getconfig',
                '/alarm/getnewnum' => '/alarm/index/getnewnum',
                '/alarm/msglist' => '/alarm/index/msglist'
                '新路由路径' => '原路径地址'

                ...

            );

            ...
            ...
        }

        _handl_url();
    ?>


