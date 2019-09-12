####################################################################################################
**资源加密**
####################################################################################################

展示给用户的资源链接都是需要加签名的，如：http://www.test.com/wq/xxx.jpg?OSSAccessKeyId=3YP0p&Signature=%2F6xalOa%2Ff&Expires=1566959718

:文件URL签名:

.. code-block:: php
    :linenos:

    <?php
        // 结果：http://xxx.jpg  =>  http://xxx.jpg?OSSAccessKeyId=3YP0p&Signature=%2F6xalOa%2Ff&Expires=1566959718
        FileUtil::getSignUrl($oss_pic_url);
    ?>

:注意问题:

在网页JS的处理过程中，网页的某些写法可能会把URL的链接中的URL特殊字符给转义，如： ``#、&`` ,这样会导致查询字符串拼接错误。阿里云直接抛出 ``AccessDenied``。

    .. code-block::
        :linenos:

        如下会把 ``&`` => ``&amp;`` ：
            正确：http://www.test.com/wq/xxx.jpg?OSSAccessKeyId=3YP0p&Signature=%2F6xalOa%2Ff&Expires=1566959718
            错误：http://www.test.com/wq/xxx.jpg?OSSAccessKeyId=3YP0p&amp;Signature=%2F6xalOa%2Ff&amp;Expires=1566959718

        JS解决方案：
            慎用 content.html() 改用 content.text()
            var str = 'http://www.test.com/wq/xxx.jpg?OSSAccessKeyId=3YP0p&amp;Signature=%2F6xalOa%2Ff&amp;Expires=1566959718'
            var url = str.replace(/&amp;/g, "&");


####################################################################################################
**资源解密**
####################################################################################################

存储到数据库的资源链接都是不带签名的，如：http://www.test.com/wq/xxx.jpg

:文件URL反签名:

.. code-block:: php
    :linenos:

    <?php
        FileUtil::aliyunUrlUnsigned($oss_pic_url);
    ?>


str.replace(/&amp;/g, "&");