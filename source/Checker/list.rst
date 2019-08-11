####################################################################################################
**验证器列表**
####################################################################################################

******************************************************************************************
**CustomChecker**
******************************************************************************************

******************************************************************************************
**DeleteCheckTableChecker**
******************************************************************************************

******************************************************************************************
**EmailChecker**
******************************************************************************************



.. code-block:: php
    :linenos:
    :emphasize-lines: 5

    <?php
        protected function getCheckers()
        {
            return [
                new EmailChecker($name, $label), // 验证邮件
            ];
        }
    ?>




******************************************************************************************
**FloatChecker**
******************************************************************************************

******************************************************************************************
**HanziChecker**
******************************************************************************************

******************************************************************************************
**IdExistChecker**
******************************************************************************************

**说明：** 验证某个表中的 ``id`` 是否存在。

**对象：** new IdExistChecker($name, $label, $table, $is_del = false)

**参数：** ``$name`` 需要验证的字段, ``$label`` 异常信息前缀, ``$table`` 需要验证的表, ``$is_del`` 是否有假删除。

.. code-block:: php
    :linenos:
    :emphasize-lines: 5

    <?php
        protected function getCheckers()
        {
            return [
                new IdExistChecker('sponsor', '主办人不存在/', \DBUtils::USER),
            ];
        }
    ?>

**显示：** 异常情况下显示的示例。

.. code-block:: 
    :linenos:
    
    11111

******************************************************************************************
**IntChecker**
******************************************************************************************

**说明：** 验证某个值（int类型）的正确性, 同时多选参数判断值域的正确性。

**对象：** new IntChecker($name, $label, $min = null, $max = null)

**参数：** ``$name`` 需要验证的字段, ``$label`` 异常信息前缀, ``$min`` 最小值域, ``$max`` 最大值域。

.. code-block:: php
    :linenos:
    :emphasize-lines: 5

    <?php
        protected function getCheckers()
        {
            return [
                new new IntChecker('post_id', '值不存在/', 1, 5),
            ];
        }
    ?>

**显示：** 异常情况下显示的示例。

.. code-block:: 
    :linenos:
    
    '值不存在/错误'   // post_id = 'string'
    '值不存在/错误'   // post_id = 0
    '值不存在/错误'   // post_id = 6

******************************************************************************************
**IpChecker**
******************************************************************************************

**说明：** 验证 ``ip地址`` 的正确性。

**对象：** new IpChecker()

**参数：** 无

.. code-block:: php
    :linenos:
    :emphasize-lines: 5

    <?php
        protected function getCheckers()
        {
            return [
                new new IpChecker('ip', '值不存在/', 1, 5),
            ];
        }
    ?>

**显示：** 异常情况下显示的示例。

.. code-block:: 
    :linenos:
    
    'ip地址不正确'   // ip = '192.168.42.256'

******************************************************************************************
**LenChecker**
******************************************************************************************

**说明：** 验证长度。

**对象：** new LenChecker($name, $label, $min = 0, $max = 0)

**参数：** ``$name`` 需要验证的字段, ``$label`` 异常信息前缀, ``$min`` 最小值域, ``$max`` 最大值域。

.. code-block:: php
    :linenos:
    :emphasize-lines: 5

    <?php
        protected function getCheckers()
        {
            return [
                new new LenChecker('post_id', '值不存在/', 1, 5),
            ];
        }
    ?>

**显示：** 异常情况下显示的示例。

.. code-block:: 
    :linenos:
    
    '值不存在/错误'   // post_id = 'string'
    '值不存在/错误'   // post_id = 0
    '值不存在/错误'   // post_id = 6


******************************************************************************************
**MustChecker**
******************************************************************************************

**说明：** 验证字段必填, 包括字符串 ``'[]'``也是空。

**对象：** new MustChecker($name, $label)

**参数：** ``$name`` 需要验证的字段, ``$label`` 异常信息前缀（此验证器中没有用到）。

.. code-block:: php
    :linenos:
    :emphasize-lines: 5

    <?php
        protected function getCheckers()
        {
            return [
                new new MustChecker('password', ''),
            ];
        }
    ?>

**显示：** 异常情况下显示的示例。

.. code-block:: 
    :linenos:
    
    '值不存在/错误'   // post_id = 'string'


******************************************************************************************
**MustSelectOneChecker**
******************************************************************************************

**说明：** 验证传入参数是否在 ``$keys`` 中存在。

**对象：** new MustSelectOneChecker($keys)

**参数：** ``$keys`` 需要验证的一维数组。

.. code-block:: php
    :linenos:
    :emphasize-lines: 5

    <?php
        protected function getCheckers()
        {
            return [
                new new MustSelectOneChecker(['jollysone', 'pwd', 21]),
            ];
        }
    ?>

**显示：** 异常情况下显示的示例。

.. code-block:: 
    :linenos:
    
    '值不存在/错误'   // post_id = 'string'

******************************************************************************************
**NameChecker**
******************************************************************************************

**说明：** 验证名称在表中某个字段是否存在。

**对象：** new NameChecker($tableName, $nameKey = 'name')

**参数：** ``$tableName`` 验证表名, ``$nameKey`` 需检查的字段。

.. code-block:: php
    :linenos:
    :emphasize-lines: 5

    <?php
        protected function getCheckers()
        {
            return [
                new new NameChecker('user', 'username'),
            ];
        }
    ?>

**显示：** 异常情况下显示的示例。

.. code-block:: 
    :linenos:
    
    '值不存在/错误'   // post_id = 'string'

******************************************************************************************
**PhoneChecker**
******************************************************************************************

**说明：** 验证某个字段是否是手机号。

**对象：** new PhoneChecker($name, $label)

**参数：** ``$name`` 验证字段, ``$label`` 异常显示信息。

.. code-block:: php
    :linenos:
    :emphasize-lines: 5

    <?php
        protected function getCheckers()
        {
            return [
                new new PhoneChecker('phone', '手机号不存在'),
            ];
        }
    ?>

**显示：** 异常情况下显示的示例。

.. code-block:: 
    :linenos:
    
    '值不存在/错误'   // post_id = 'string'


******************************************************************************************
**PictTextMustChecker**
******************************************************************************************

**说明：** 验证是否是图片json格式的文本。

**对象：** new PictTextMustChecker($name, $label)

**参数：** ``$name`` 验证字段, ``$label`` 异常显示信息。

.. code-block:: php
    :linenos:
    :emphasize-lines: 5

    <?php
        protected function getCheckers()
        {
            return [
                new new PictTextMustChecker('pic', '图片不正确'),
            ];
        }
    ?>

**显示：** 异常情况下显示的示例。

.. code-block:: 
    :linenos:
    
    '值不存在/错误'   // post_id = 'string'


******************************************************************************************
**TimeRangeChecker**
******************************************************************************************

**说明：** 判断开始时间不能大于结束时间（ ``仅限于判断时间戳`` ）。

**对象：** new TimeRangeChecker($name, $label, $end_name)

**参数：** ``$name`` 开始时间字段, ``$label`` 异常显示信息, ``$end_name`` 结束时间字段。

.. code-block:: php
    :linenos:
    :emphasize-lines: 5

    <?php
        protected function getCheckers()
        {
            return [
                new new TimeRangeChecker('1565512523', '开始时间不能大于结束时间', '1565512522'),
            ];
        }
    ?>

**显示：** 异常情况下显示的示例。

.. code-block:: 
    :linenos:
    
    '开始时间不能大于结束时间'   // post_id = 'string'

******************************************************************************************
**TimeRangeConflictChecker**
******************************************************************************************

**说明：** 判断开始时间不能大于结束时间（ ``仅限于判断时间戳`` ）。

**对象：** new TimeRangeConflictChecker($start_name, $end_name, $table_name, $params_arr, $label)

**参数：** ``$start_name`` 开始时间字段, ``$end_name`` 结束时间字段, ``$table_name`` 表名, ``$params_arr`` 参数数组, ``$label`` 异常显示信息

.. code-block:: php
    :linenos:
    :emphasize-lines: 5

    <?php
        protected function getCheckers()
        {
            return [
                new new TimeRangeConflictChecker('1565512523', '开始时间不能大于结束时间', '1565512522'),
            ];
        }
    ?>

**显示：** 异常情况下显示的示例。

.. code-block:: 
    :linenos:
    
    '开始时间不能大于结束时间'   // post_id = 'string'

******************************************************************************************
**UniqueChecker**
******************************************************************************************

**说明：** 判断开始时间不能大于结束时间（ ``仅限于判断时间戳`` ）。

**对象：** new UniqueChecker($name, $label = '', $table, $id, $db_name = '')

**参数：** ``$name`` 需判断的字段, ``$label`` 异常显示信息, ``$table`` 表名, ``$id`` 值, ``$db_name`` 数据库名, 

.. code-block:: php
    :linenos:
    :emphasize-lines: 5

    <?php
        protected function getCheckers()
        {
            return [
                new new UniqueChecker('1565512523', '开始时间不能大于结束时间', '1565512522'),
            ];
        }
    ?>

**显示：** 异常情况下显示的示例。

.. code-block:: 
    :linenos:
    
    '开始时间不能大于结束时间'   // post_id = 'string'

