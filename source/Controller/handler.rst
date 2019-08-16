####################################################################################################
**流程处理器**
####################################################################################################

******************************************************************************************
**列表处理器**
******************************************************************************************

================================================================================
**onListBefore(&$list)**
================================================================================

**适用：** ``ListAction``  ``DetailAction``

**说明：** 在渲染列表前需要进行数据处理。数组内可以传入多个，执行顺序按数组索引顺序。

.. note::
    **第一步：** 新建流程处理类对象处理列表数据的引用。（需实现 ``IListBeforeHandler`` 方法）

    .. code-block:: php
        :linenos:

            <?php
                class ExampleListBeforeHandler implements IListBeforeHandler
                {
                    public function onListBefore(&$list, CRequest $request, $action)
                    {
                        foreach($list as $k => $v){

                            ...

                            $list[$k]['unixtime'] = time(); // 处理增加一个额外时间
                            
                            ...
                        }
                    }
                }
            ?>


    **第二步：** 将流程处理类添加到数组中即可。

        .. code-block:: php
            :linenos:

            <?php
                protected function onListBefore(&$list)
                {
                    return [
                        ...

                        new ExampleListBeforeHandler(),

                        ...
                    ];
                }
            ?>
 
 .. Tip:: 

    1. 需要其它配合参数可通过 ``__construct()`` 进行传入。
    2. 第二步数组内可以传入多个，执行顺序按数组索引顺序。



******************************************************************************************
**保存处理器**
******************************************************************************************

================================================================================
**onBeforeSave(&$data)**
================================================================================

**适用：** ``SaveAction``

**说明：** 在保存前需要进行数据处理。数组内可以传入多个，执行顺序按数组索引顺序。

.. note::
    **第一步：** 新建流程处理类对象处理列表数据的引用。（需实现 ``ISaveBeforeHandler`` 方法）

        .. code-block:: php
            :linenos:

            <?php
                class ExampleSaveBeforeHandler implements ISaveBeforeHandler
                {
                    public function onSaveBefore(&$data, CRequest $request, $is_add, $action)
                    {
                        ...

                        $data['unixtime'] = time(); // 处理增加一个额外时间

                        ...
                    }
                }
            ?>


    **第二步：** 将流程处理类添加到数组中即可。

        .. code-block:: php
            :linenos:

            <?php
                protected function onBeforeSave(&$data)
                {
                    return [
                        ...

                        new ExampleSaveBeforeHandler(),
                        
                        ...
                    ];
                }
            ?>

.. Tip:: 

    1. 需要其它配合参数可通过 ``__construct()`` 进行传入。
    2. 第二步数组内可以传入多个，执行顺序按数组索引顺序。




================================================================================
**onAfterSave($data)**
================================================================================

**适用：** ``SaveAction``

**说明：** 在保存前需要进行数据处理。数组内可以传入多个，执行顺序按数组索引顺序。

.. note::
    **第一步：** 新建流程处理类对象处理列表数据的引用。（需实现 ``ISaveAfterHandler`` 方法）

        .. code-block:: php
            :linenos:

            <?php
                class ExampleSaveAfterHandler implements ISaveAfterHandler
                {
                    public function onSaveAfter(&$data, CRequest $request, $is_add, $old_data, $action)
                    {
                        ...

                        $data['unixtime'] = time(); // 处理增加一个额外时间

                        ...
                    }
                }
            ?>


    **第二步：** 将流程处理类添加到数组中即可。

        .. code-block:: php
            :linenos:

            <?php
                protected function onAfterSave($data)
                {
                    return [
                        ...

                        new ExampleSaveAfterHandler(),
                        
                        ...
                    ];
                }
            ?>


.. Tip:: 

    1. 需要其它参数配合可通过 ``__construct()`` 进行传入。处理过程中还可以使用更多的参数 ``$is_add`` ``$old_data`` 。
    2. 第二步数组内可以传入多个，执行顺序按数组索引顺序。


******************************************************************************************
**删除处理器**
******************************************************************************************

================================================================================
**onBeforeDelete(&$data)**
================================================================================

**适用：** ``DeleteAction``

**说明：** 在保存前需要进行数据处理。数组内可以传入多个，执行顺序按数组索引顺序。

.. note::
    **第一步：** 新建流程处理类对象处理列表数据的引用。（需实现 ``IDeleteBeforeHandler`` 方法）

        .. code-block:: php
            :linenos:

            <?php
                class ExampleSaveBeforeHandler implements IDeleteBeforeHandler
                {
                    public function onDeleteBefore(&$data, CRequest $request, $action)
                    {
                        ...

                        $data['unixtime'] = time(); // 处理增加一个额外时间

                        ...
                    }
                }
            ?>

    **第二步：** 将流程处理类添加到数组中即可。

        .. code-block:: php
            :linenos:

            <?php
                protected function onBeforeDelete(&$data)
                {
                    return [
                        ...

                        new ExampleDeleteBeforeHandler(),
                        
                        ...
                    ];
                }
            ?>

.. Tip:: 

    1. 需要其它配合参数可通过 ``__construct()`` 进行传入。
    2. 第二步数组内可以传入多个，执行顺序按数组索引顺序。


================================================================================
**onAfterDelete(&$data)**
================================================================================

**适用：** ``DeleteAction``

**说明：** 在保存前需要进行数据处理。数组内可以传入多个，执行顺序按数组索引顺序。

.. note::
    **第一步：** 新建流程处理类对象处理列表数据的引用。（需实现 ``IDeleteAfterHandler`` 方法）

        .. code-block:: php
            :linenos:

            <?php
                class ExampleSaveBeforeHandler implements ISaveBeforeHandler
                {
                    public function onDeleteAfter(&$data, CRequest $request, $action)
                    {
                        ...

                        $data['unixtime'] = time(); // 处理增加一个额外时间

                        ...
                    }
                }
            ?>

    **第二步：** 将流程处理类添加到数组中即可。

        .. code-block:: php
            :linenos:

            <?php
                protected function onAfterDelete(&$data)
                {
                    return [
                        ...

                        new ExampleDeleteBeforeHandler(),
                        
                        ...
                    ];
                }
            ?>


.. Tip:: 

    1. 需要其它配合参数可通过 ``__construct()`` 进行传入。
    2. 第二步数组内可以传入多个，执行顺序按数组索引顺序。
    


