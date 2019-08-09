####################################################################################################
**入口文件**
####################################################################################################

应用入口文件位于： **project/index.php**

内容如下：

.. code-block:: php
    :linenos:

    <?php
        date_default_timezone_set('Asia/Shanghai');
        ini_set('display_errors', true);error_reporting(E_ALL  ^  E_NOTICE );

        include __DIR__.'/../CC2/CC.php';
        $app = include  __DIR__.'/protected/pre/app.php';
        $app->run();
    ?>




