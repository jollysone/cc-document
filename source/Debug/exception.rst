####################################################################################################
**异常**
####################################################################################################

******************************************************************************************
**捕获异常**
******************************************************************************************

如何捕获异常

**参数：** **new CErrorException(** $message = null, $code = 10000, $other_arr = array() **)**

**参数：** 

    **$message：** 异常信息，

    **$code：** 异常错误代码，

    **$other_arr：** 错误的其它数组信息。

**例1：**

.. code-block:: php

    <?php
        throw new CErrorException('页面输入错误!');
    ?>
