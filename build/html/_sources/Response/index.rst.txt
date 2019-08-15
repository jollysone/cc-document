####################################################################################################
**响应为Json格式**
####################################################################################################

**代码示例**

.. code-block:: php
    :linenos:

    <?php
        class TaskApiAction extends \CAction
        {
            public function execute(CRequest $request)
            {
                return new \CJsonData([
                    'id' => 1,
                    'name' => 'jollysone',
                    'age' => 24
                ]);
            }
        }
    ?>

**结果示例**

.. code-block:: json
    :linenos:

    {
        "ok": true,
        "servertime": 1565342212,
        "id": 1,
        "name": "jollysone",
        "age": 24
    }


####################################################################################################
**响应为Jsonp格式**
####################################################################################################

**代码示例**

.. code-block:: php
    :linenos:

    <?php

        class TaskApiAction extends \CAction
        {
            public function execute(CRequest $request)
            {
                return new \CJsonpData([
                    'id' => 1,
                    'name' => 'jollysone',
                    'age' => 24
                ]);
            }
        }
    ?>

**结果示例**

.. code-block:: 
    :linenos:

    ({
        "ok":true,
        "servertime":1565342395,
        "id":1,
        "name":"jollysone",
        "age":24
    })

####################################################################################################
**响应为Render格式**
####################################################################################################

第一个参数是 传给视图文件的变量

第二参数是 视图文件的名字

第三个参数是 是否使用布局文件

第四个参数是 布局文件的路径

    return new CRenderData($data, $view, $isLayout, $layouts, $view_dir);

####################################################################################################
**响应空数据格式**
####################################################################################################

**代码示例**

.. code-block:: php
    :linenos:

    <?php

        public function execute(CRequest $request)
        {
            return new \CNoneData();
        }

    ?>

**结果示例**

.. code-block:: php
    :linenos:

    // 响应为空, 什么内容都没有
