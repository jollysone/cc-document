####################################################################################################
**过滤器**
####################################################################################################

******************************************************************************************
**基本用法**
******************************************************************************************

过滤器视图通常需要跟服务端搭配使用。视图中渲染的各种 ``过滤器组件`` , 详见本章其它小节。

.. note:: 
    **重要的三步：**

    1. 在控制器中实现 ``ITableViewCreator`` 的 ``createListFilters()`` 方法。

    2. 在 ``createListFilters()`` 方法中实例化各种组件, 并且以 ``数组形式`` 返回。

    3. 在同级目录的 ``view`` 文件中渲染视图内容。

**控制器写法：**

.. code-block:: php
    :linenos:
    :emphasize-lines: 2,6-10

    <?php
        class ExampleManageIndexAction extends ListAction implements ITableViewCreator
        {
            ...
            
            public function createListFilters()
            {
                $filters[] = new TimeRangeFilter('assign_time', '指派时间', 'simple');
                return $filters;
            }

            ...
        }
    ?>

**视图文件写法：**

.. code-block:: php
    :linenos:
    :emphasize-lines: 6

    <?php
        use CC\util\common\widget\panel\ListSearchPanel;
        use CC\util\common\widget\widget\FilterWidget;
        use CC\util\common\widget\widget\WidgetBuilder;

        echo WidgetBuilder::build(new FilterWidget($this), ListSearchPanel::instance());
    ?>

******************************************************************************************
**过滤器样式**
******************************************************************************************

默认样式是垂直显示方式（ **'style' => 'vertical'** ）。

================================================================================
**水平排列风格**
================================================================================

.. code-block:: php
    :linenos:
    :emphasize-lines: 6

    <?php
        use CC\util\common\widget\panel\ListSearchPanel;
        use CC\util\common\widget\widget\FilterWidget;
        use CC\util\common\widget\widget\WidgetBuilder;

        echo WidgetBuilder::build(new FilterWidget($this, ['style' => 'horizontal']), ListSearchPanel::instance());
    ?>


================================================================================
**垂直排列风格**
================================================================================

.. code-block:: php
    :linenos:
    :emphasize-lines: 6

    <?php
        use CC\util\common\widget\panel\ListSearchPanel;
        use CC\util\common\widget\widget\FilterWidget;
        use CC\util\common\widget\widget\WidgetBuilder;

        echo WidgetBuilder::build(new FilterWidget($this, ['style' => 'vertical']), ListSearchPanel::instance());
    ?>


******************************************************************************************
**过滤器组件**
******************************************************************************************

================================================================================
**文本输入框**
================================================================================

.. code-block:: php
    :linenos:

    <?php
        $filters[] = new InputFilter($name, $label, $placeholder, $is_show_submit, [
            'is_need_setting' => false,
            'is_need_reset' => true,
        ]);
    ?>


================================================================================
**单选框 & 复选框**
================================================================================

**方法：** **new SelectFilter(** $name, $label, $data_arr, $style = '', $default_option = [] **)**

**参数：** 

    **$name：** ``必填`` 字段名，

    **$label：** ``必填`` 标签显示名称，

    **$data_arr：** ``必填`` 选择框数据（一维数组），

    **$style：** 选择框样式（ **'', 'multi', 'drop-down', 'drop-pop'** ）默认第一个，

    **$default_option：** 额外配置默认选择的一项 **['value' => 'showText']**，默认不选择。

**扩展方法：** 设置是否多选，只适用于 ``$style：'' | 'multi'`` 的场景。

.. code-block:: php
    :linenos:

    <?php
        $filters[] = (new SelectFilter($name, $label, $data_arr))->setIsMultiple(bool);
    ?>


**例1：** 配置 $style = 'multi' 或者 $style = ''，支持单选、多选双模式。

.. image:: ../_static/view_filter_select_1.png
    :height: 62px
    :alt: view_filter_select_1
    :align: center

.. Tip:: 
    需要保持这个样式但是只需要单选功能，可配置扩展方法（ **setIsMultiple(false)** ）设置单选;

**例2：** 配置 $style = 'drop-down' ，单选，不自动跳转。

.. image:: ../_static/view_filter_select_2.png
    :height: 128px
    :alt: view_filter_select_2
    :align: center

**例3：** 配置 $style = 'drop-pop' ，单选，自动跳转。

.. image:: ../_static/view_filter_select_3.png
    :height: 130px
    :alt: view_filter_select_3
    :align: center


================================================================================
**时间范围**
================================================================================

**方法：** **new TimeRangeFilter(** $name, $label, $style = '', $ranges = null, $option = [] **)**

**参数：** 

    **$name：** ``必填`` 字段名，

    **$label：** ``必填`` 标签显示名称，

    **$style：** 选择框样式（ **'', 'simple'** ）默认第一个，
    
    **$ranges：** 默认 **['total', 'today', 'this_week', 'this_month']**，

    **$option：** 额外配置默认选择项 **['default_choose' => 'total']**，默认不选择。

.. note::
    **$ranges** 可配置的可选项。
    
        1. 'total' 全部,
        2. 'today' 今日,
        3. 'this_week' 本周,
        4. 'this_month' 本月,
        5. 'yesterday' 昨日,
        6. 'last_week' 上周,
        7. 'last_month' 上一月,

**扩展方法：**  。

.. code-block:: php
    :linenos:

    <?php
        $filters[] = (new SelectFilter($name, $label, $data_arr))->setIsMultiple(bool);
    ?>


**例1：** 配置 $style = 'multi' 或者 $style = ''，支持单选、多选双模式。

.. image:: ../_static/view_filter_select_1.png
    :height: 62px
    :alt: view_filter_select_1
    :align: center

.. code-block:: php
    :linenos:

    <?php
        /** $style 可取 '', 'simple'
          * '' 含快捷标签
          * 'simple' 只有开始和结束时间
          * $ranges 默认取值 ['total','today','this_week','this_month']
          * $ranges 所有可取值 ['total','today','this_week','this_month','yesterday','last_week','last_month']
        */

        $filters[] = new TimeRangeFilter($name, $label, $style, $ranges)
    ?>


================================================================================
**时间点**
================================================================================

**方法：** 

**new SimpleTimeFilter(** $name, $label, $placeholder, $style = '', $end_min = false, $end_max = false **)**

**参数：** 

    **$name：** ``必填`` 字段名，

    **$label：** ``必填`` 标签显示名称，

    **$placeholder：**  ``必填`` 描述输入字段预期值的提示信息，

    **$style：**  配置该组件的 class ，选择月份 ``'date-month'`` 选择年份 ``'date-year'`` 默认选择日期，

    **$end_min：** 可选择的最早时间是否从当前开始，

    **$end_max：** 可选择的最晚时间是否从当前结束。


**例1：** 配置 $style = '' 或者 不配置，日期的选择。

.. image:: ../_static/view_filter_simple_time_1.png
    :height: 240px
    :alt: view_filter_simple_time_1
    :align: center

**例2：** 配置 $style = 'date-month' ，可按月份选择。

.. image:: ../_static/view_filter_simple_time_2.png
    :height: 231px
    :alt: view_filter_simple_time_2
    :align: center

**例3：** 配置 $style = 'date-year' ，可按年份选择。

.. image:: ../_static/view_filter_simple_time_3.png
    :height: 237px
    :alt: view_filter_simple_time_3
    :align: center


================================================================================
**范围过滤器**
================================================================================

.. code-block:: php
    :linenos:

    <?php
        $filters[] = new RangeInputFilter();
    ?>


================================================================================
**树结构过滤器**
================================================================================

.. code-block:: php
    :linenos:

    <?php
        $filters[] = new TreeFilter($name, $label, $data_arr, [
            'is_multi' => true,
            'only_child' => false,
            'position' => 'fixed'
        ]);
    ?>






******************************************************************************************
**自定义过滤器**
******************************************************************************************


.. code-block:: php
    :linenos:

    <?php
        use CC\util\common\widget\filter\FilterAbs;

        class CustomFilter extends FilterAbs
        {

            protected function onCreateFilter(\CRequest $request)
            {
                return [

                ];
            }
        }
    ?>


