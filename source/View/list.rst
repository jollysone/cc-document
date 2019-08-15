####################################################################################################
**列表**
####################################################################################################

******************************************************************************************
**基本用法**
******************************************************************************************


列表字段配置

操作按钮配置

================================================================================
**配置表格字段**
================================================================================

**例1：**

.. code-block:: php
    :linenos:

    <?php
        public function createListColumns(array $list)
        {
            $is_export = $this->isExport();

            $columns[] = new Column('主办人', 'sponsor_name');
            $columns[] = new Column('协办人', 'co_sponsor_name', function ($data) use ($is_export){
                if ($is_export){
                    return $data['co_sponsor_name'];
                }else{
                    return new SplitColumnValueSetter('co_sponsor_name',15);
                }
            });
            $columns[] = new Column('状态', 'sub_status', function ($data){
                switch ($data['sub_status']){
                    case TaskOpTypeEnum::WAIT_LOOK:
                        $msg = '待查看';
                        break;
                    case TaskOpTypeEnum::WAIT_HANDLE:
                        $msg = '待处理';
                        break;
                    case TaskOpTypeEnum::HANDLING:
                        $msg = '处理中';
                        break;
                    default:
                        $msg = '未知状态';
                        break;
                }
                return $msg;
            });

            return $columns;
        }
    ?>



******************************************************************************************
**自定义表格**
******************************************************************************************

**视图文件**

.. code-block:: php
    :linenos:
    :emphasize-lines: 1

    <?php
        use CC\util\common\widget\widget\PagingWidget;
        use CC\util\common\widget\widget\WidgetBuilder;
        $titleData = array_splice($list, 0, 1);

        $titleList = [];
        foreach ($titleData as $k => $v) {
            foreach ($v as $item) {
                $titleList[] = $item['value'];
            }
        }

        $titleCount = count($titleList) + ($is_show_btn ? 1 : 0) + ($options['is_show_sequence'] ? 1 : 0);
    ?>

    <table id="<?php echo $options['id']; ?>" class="table">
        <thead>
            <tr>
                <?php if($options['is_show_sequence']):?>
                    <th><?php echo CC::t('view_ordinal');?></th>
                <?php endif;?>

                <?php foreach ($titleList as $title): ?>
                    <th><?php echo $title ;?></th>
                <?php endforeach ?>

                <?php if ($is_show_btn): ?>
                    <th style="min-width: 24px;"><?php echo $options['op_btn_name'];?></th>
                <?php endif; ?>
            </tr>
        </thead>
        <tbody>
                <?php foreach ($list as $k => $item): ?>
                    <tr data-id="<?php echo $item['orgi_data']['id']?>">
                    <?php
                        if ($options['is_show_sequence']) {
                            echo '<td>' . ($page ? ($k + $page->curPage * $page->pageSize + 1) : ($k + 1)) . '</td>';
                        }
                    ?>

                    <?php foreach ($item['datas'] as $data):?>
                        <?php $style = $data['options']['td_style'] ? $data['options']['td_style'] : ''; ?>
                        <td <?php echo 'style="' . $style . '"'; ?>><?php echo $data['value'] ?></td>
                    <?php endforeach ?>

                    <?php if($is_show_btn):?>
                    <?php $btn_str = WidgetBuilder::build($op_data_widget->setData($list_orig[$k])); ?>
                    <td class="table_op_td" <?php /**trick**/ echo isset($style) ? 'style="' . $style . '"' : ''; ?>>
                        <?php echo $btn_str ? $btn_str : '无'; ?>
                    </td>
                    <?php endif;?>
                    </tr>
                <?php endforeach ?>
        </tbody>
    </table>

    <?php
        if ($options['is_show_page'] && $page) {
            echo WidgetBuilder::build(new PagingWidget($page, $options['is_show_page_num'], $options['is_change_page_ajax'], $options['is_change_page_num_ajax']));
        }
    ?>


**表格控制器**

.. code-block:: php
    :linenos:

    <?php
        class GroupListTableWidget extends ListTableWidget
        {
            protected function getCalledCalsss()
            {
                return __CLASS__;
            }
        }
    ?>
