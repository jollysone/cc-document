####################################################################################################
**导入文件**
####################################################################################################

******************************************************************************************
**导入Excel文件**
******************************************************************************************

导入Excel文件

####################################################################################################
**导出文件**
####################################################################################################

******************************************************************************************
**导出配置**
******************************************************************************************

**配置文件：** protected/biz/diyField/DefaultListField.php

**注意事项：** 需要导出的 ``Action`` 不能为 ``xxxAdminAction``, 直接写为 ``xxxAction`` 即可。

**配置示例：** 给 ``unaccept`` 模块配置两个需要导出的字段( **'work_num', 'name'** )。 (模块需要在 **视图** 和 **控制器** 中对应)

.. code-block:: php
    :linenos:
    :emphasize-lines: 5,11-37

    <?php

        class DefaultListField implements IDefaultListField
        {
            const MISSION_MANAGE_UNACCEPT = "unaccept"; // 模块名

            public function getDefaultListFieldByListName($list_name)
            {
                $default_list = [];
                
                switch ($list_name) {
                    case self::MISSION_MANAGE_UNACCEPT:
                        $default_list = array(
                            "work_num" => array(
                                "name" => "工作编号", // 配置项显示名字
                                "is_system" => "1",
                                "is_use" => "1",
                                "sort" => "1",
                                "is_export" => "1", // 默认勾选是否导出
                                "export_name" => "工作编号", // 导出后标题显示名字
                                "export_sort" => "1"
                            ),
                            "name" => array(
                                "name" => "工作名称",
                                "is_system" => "1",
                                "is_use" => "1",
                                "sort" => "1",
                                "is_export" => "1",
                                "export_name" => "工作名",
                                "export_sort" => "1"
                            ),

                            ...

                        );
                        break;

                    ...

                    ...

                }

                return $default_list;
            }

        }

    ?>

******************************************************************************************
**导出Excel文件**
******************************************************************************************

**导出Excel文件**

.. code-block:: php
    :linenos:

    <?php

        protected function supportGroups()
        {
            return 'admin,cmd';
        }

        protected function isExport()
        {
            return \CC::app()->url->getGroup() == \CEnv::RUN_CMD;
        }

        protected function onExecExport($list)
        {
            $excel_data = ExcelBuilder::build($this, $list, [
                new CustomFieldColumnBuildBeforeHandler('unaccept', [
                    'is_export_field' => true
                ])
            ]);

            FileExportServer::asyncExportExcel($excel_data, '待处理任务导出表', false);

            return new \CNoneData();
        }









         protected function onExecExport($list) {    
            $excel_data = ExcelBuilder::build($this, $list);
            return Excel::instance($excel_data)->setExportDirForFlag()->createExeclForDown('xx', 'xx.zip');

            尚未完善


            $excel_data = ExcelBuilder::build($this, $list, [new CustomFieldColumnBuildBeforeHandler('xxx', ['is_export_field' => true])]);
            FileExportServer::asyncExportExcel($excel_data, 'xxx导出表', false);

            return new \CNoneData();
        }
    ?>

