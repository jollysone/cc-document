####################################################################################################
**视图**
####################################################################################################

******************************************************************************************
**视图用法**
******************************************************************************************

================================================================================
**自定义表格**
================================================================================

**视图文件**

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


class GroupListTableWidget extends ListTableWidget
{
    protected function getCalledCalsss()
    {
        return __CLASS__;
    }
}