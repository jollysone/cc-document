####################################################################################################
**视图**
####################################################################################################

******************************************************************************************
**视图用法**
******************************************************************************************

================================================================================
**过滤器**
================================================================================

**水平排列风格**

use CC\util\common\widget\panel\ListSearchPanel;
use CC\util\common\widget\widget\FilterWidget;
use CC\util\common\widget\widget\WidgetBuilder;

echo WidgetBuilder::build(new FilterWidget($this, ['style' => 'horizontal']), ListSearchPanel::instance());

**垂直排列风格**

use CC\util\common\widget\panel\ListSearchPanel;
use CC\util\common\widget\widget\FilterWidget;
use CC\util\common\widget\widget\WidgetBuilder;

echo WidgetBuilder::build(new FilterWidget($this, ['style' => 'vertical']), ListSearchPanel::instance());

**文本输入框**

new InputFilter($name, $label, $placeholder, $is_show_submit, [
    'is_need_setting' => false,
    'is_need_reset' => true,
]);

**单选框、复选框**

/** 
  * $style 可取 '', 'drop-down', 'drop-pop'
  * '' 支持单选、多选双模式
  * 'drop-down' 单选，不自动跳转
  * 'drop-pop' 单选，自动跳转
  * $default_option [value => showText]
*/
new SelectFilter($name, $label, $data_arr, $style, $default_option)

**时间范围**

// $style 可取 '', 'simple'
// '' 含快捷标签
// 'simple' 只有开始和结束时间
// $ranges 默认取值 ['total','today','this_week','this_month']
// $ranges 所有可取值 ['total','today','this_week','this_month','yesterday','last_week','last_month']
new TimeRangeFilter($name, $label, $style, $ranges)

**时间点**

new SimpleTimeFilter($name, $label, $placeholder)

**范围过滤器**

RangeInputFilter


**树过滤器**

new TreeFilter($name, $label, $data_arr, [
    'is_multi' => true,
    'only_child' => false,
    'position' => 'fixed'
])

******************************************************************************************
**自定义过滤器**
******************************************************************************************

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