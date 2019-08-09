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
