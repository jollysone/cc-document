####################################################################################################
**验证器列表**
####################################################################################################

******************************************************************************************
**CustomChecker**
******************************************************************************************

**说明：** 尚未验证用法。

**对象：** **new CustomChecker(** $name, $label, $action, $checkerName, $params **)**

**参数：** **$name：** 需验证字段， **$label：** 异常信息， **$action** xxxx， **$checkerName** xxxx， **$params** xxxx。

.. code-block:: php
    :linenos:
    :emphasize-lines: 5

    <?php
        protected function getCheckers()
        {
            return [
                new CustomChecker($name, $label, $action, $checkerName, $params),
            ];
        }
    ?>

**显示：** 异常情况下显示的示例。

.. code-block:: 
    :linenos:
    
    xxxxxxxxxxxx

******************************************************************************************
**EmailChecker**
******************************************************************************************

**说明：** 验证电子邮箱是否正确。（ **/^[a-z0-9.\-_+]+@[a-z0-9\-_]+(.[a-z0-9\-_]+)+$/i** ）

**对象：** **new EmailChecker(** $name, $label **)**

**参数：** **$name** 需验证字段，  **$label** 异常信息。

.. code-block:: php
    :linenos:
    :emphasize-lines: 5

    <?php
        protected function getCheckers()
        {
            return [
                new EmailChecker($name, $label),
            ];
        }
    ?>

**显示：** 异常情况下显示的示例。

.. code-block:: 
    :linenos:
    
    尚未验证


******************************************************************************************
**FloatChecker**
******************************************************************************************

**说明：** 验证是否是浮点数（包含了整数, 验证范围时 **不包含等于的情况** ）。（ **/^-?\d+(,\d{3,4})*(\.\d+)?$/** ）

**对象：** **new FloatChecker(** $name, $label, $min = null, $max = null **)**

**参数：** **$name** 需验证字段， **$label** 异常信息， **$min** 验证字段的最小边界， **$max** 验证字段的最大边界。

.. code-block:: php
    :linenos:
    :emphasize-lines: 5

    <?php
        protected function getCheckers()
        {
            return [
                new FloatChecker('num', '浮点数错误'), // 只验证是否浮点数
                new FloatChecker('num', '浮点数错误', 12.5, 35), // 验证是否浮点数及范围 
            ];
        }
    ?>

**显示：** 异常情况下显示的示例。

.. code-block:: 
    :linenos:
    
    尚未验证

******************************************************************************************
**HanziChecker**
******************************************************************************************

**说明：** 验证是否是汉字。（ **/^[\x{4e00}-\x{9fa5}]+$/u** ）

**对象：** **new HanziChecker(** $name, $label **)**

**参数：** **$name** 需验证字段， **$label** 异常信息。

.. code-block:: php
    :linenos:
    :emphasize-lines: 5

    <?php
        protected function getCheckers()
        {
            return [
                new HanziChecker('sponsor', '只能填写汉字'),
            ];
        }
    ?>

**显示：** 异常情况下显示的示例。

.. code-block:: 
    :linenos:
    
    尚未验证

******************************************************************************************
**IdExistChecker**
******************************************************************************************

**说明：** 验证某个表中的 ``id`` 是否存在。

**对象：** **new IdExistChecker(** $name, $label, $table, $is_del = false **)**

**参数：** **$name** 需验证字段， **$label** 异常信息, **$table** 需验证的表, **$is_del** 是否假删除。

.. code-block:: php
    :linenos:
    :emphasize-lines: 5

    <?php
        protected function getCheckers()
        {
            return [
                new IdExistChecker('sponsor_id', '主办人不存在/', 'user'), // sponsor_id 在 user 表 id 中不存在
            ];
        }
    ?>

**显示：** 异常情况下显示的示例。

.. code-block:: 
    :linenos:
    
    尚未验证

******************************************************************************************
**IntChecker**
******************************************************************************************

**说明：** 验证是否整数，验证范围时 **不包含等于的情况** 。（ **/^\d+$/** ）

**对象：** **new IntChecker(** $name, $label, $min = null, $max = null **)**

**参数：** **$name** 需验证字段， **$label** 异常信息， **$min** 最小值域， **$max** 最大值域。

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
    
    尚未验证

******************************************************************************************
**IpChecker**
******************************************************************************************

**说明：** 验证 ``ip地址`` 的正确性。

**对象：** **new IpChecker(** $name, $label **)**

**参数：** **$name** 需验证字段， **$label** 异常信息。

.. code-block:: php
    :linenos:
    :emphasize-lines: 5

    <?php
        protected function getCheckers()
        {
            return [
                new new IpChecker('ip', 'ip地址不正确/'),
            ];
        }
    ?>

**显示：** 异常情况下显示的示例。

.. code-block:: 
    :linenos:
    
    尚未验证

******************************************************************************************
**LenChecker**
******************************************************************************************

**说明：** 验证字符串长度是否在范围内。（ **mb_strlen($val,'utf-8')** ）

**对象：** **new LenChecker(** $name, $label, $min = 0, $max = 0 **)**

**参数：** **$name** 需验证字段， **$label** 异常信息， **$min** 最小值域， **$max** 最大值域。

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
    
    尚未验证


******************************************************************************************
**MustChecker**
******************************************************************************************

**说明：** 验证字段必填, 包括字符串 ``'[]'`` 也是空。

**对象：** **new MustChecker(** $name, $label **)**

**参数：** **$name** 需验证字段， **$label** 异常信息。

.. code-block:: php
    :linenos:
    :emphasize-lines: 5

    <?php
        protected function getCheckers()
        {
            return [
                new new MustChecker('password', '密码不能为空'),
            ];
        }
    ?>

**显示：** 异常情况下显示的示例。

.. code-block:: 
    :linenos:
    
    尚未验证


******************************************************************************************
**MustSelectOneChecker**
******************************************************************************************

**说明：** 验证传入参数是否在 ``$keys`` 中存在。

**对象：** **new MustSelectOneChecker(** $keys **)**

**参数：** **$keys** 需要验证的 **一维索引数组** 。

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
    
    尚未验证

******************************************************************************************
**NameChecker**
******************************************************************************************

**说明：** 验证名称在表中某个字段是否存在，一般用于判重。

**对象：** **new NameChecker(** $tableName, $nameKey = 'name' **)**

**参数：** **$tableName** 验证表名， **$nameKey** 需检查的字段。

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
    
    尚未验证

******************************************************************************************
**PhoneChecker**
******************************************************************************************

**说明：** 验证是否是手机号。（ **/^1[345789]\d{9}$/** ）

**对象：** **new PhoneChecker(** $name, $label **)**

**参数：** **$name** 需验证字段， **$label** 异常信息。

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
    
    尚未验证


******************************************************************************************
**PictTextMustChecker**
******************************************************************************************

**说明：** 验证是否是图片json格式的文本。 尚未搞清具体功能----------

**对象：** **new PictTextMustChecker(** $name, $label **)**

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
    
    尚未验证


******************************************************************************************
**TimeRangeChecker**
******************************************************************************************

**说明：** 判断开始时间不能大于结束时间（ ``仅限于判断时间戳`` ）。

**对象：** **new TimeRangeChecker(** $name, $label, $end_name **)**

**参数：** **$name** 开始时间字段， **$label** 异常显示信息， **$end_name** 结束时间字段。

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
    
    尚未验证

******************************************************************************************
**TimeRangeConflictChecker**
******************************************************************************************

**说明：** 判断时间是否冲突（ ``仅限于判断时间戳`` ）。

**对象：** **new TimeRangeConflictChecker(** $start_name, $end_name, $table_name, $params_arr, $label **)**

**参数：** **$start_name** 开始时间字段， **$end_name** 结束时间字段， **$table_name** 表名， **$params_arr** 参数数组， **$label** 异常显示信息。

.. code-block:: php
    :linenos:
    :emphasize-lines: 5-10

    <?php
        protected function getCheckers()
        {
            return [
                new new TimeRangeConflictChecker('1565512523', '1565513613', 'activity', [
                    'is_tmp' => 1

                    ...
                    
                ], '所选时间有冲突'),
            ];
        }
    ?>

.. code-block:: php
    :linenos:

    // 核心原理
    <?php
        $sections_model = ListModel::make($this->table_name)->addColumnsCondition($this->params_arr)->execute();
        $message = $this->getMessage();
        foreach($sections_model as $section){
            if($section['id'] == $this->id){
                continue;
            }
            if($new_start_time >= $section['start_time'] && $new_start_time <= $section['end_time']){
                $msg = $message[0];
                return false;
            }
            if($new_end_time >= $section['start_time'] && $new_end_time <= $section['end_time']){
                $msg = $message[1];
                return false;
            }
            if($new_start_time <= $section['start_time'] && $new_end_time >= $section['end_time']){
                $msg = $message[2];
                return false;
            }
        }
    ?>

**显示：** 异常情况下显示的示例。

.. code-block:: 
    :linenos:
    
    尚未验证

******************************************************************************************
**UniqueChecker**
******************************************************************************************

**说明：** 判断是否唯一。

**对象：** **new UniqueChecker(** $name, $label = '', $table, $id, $db_name = '', $id_name = 'id' **)**

**参数：** **$name** 需验证字段， **$label** 异常信息， **$table** 表名， **$id** 值， **$db_name** 数据库名, **$id_name** 主键名字

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
    
    尚未验证

