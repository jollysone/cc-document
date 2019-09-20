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


******************************************************************************************
**网页录音文件转MP3**
******************************************************************************************

**导出Excel文件**

.. code-block:: php
    :linenos:

    <?php
        $mp3filepath = '/tmp/mp3' . md5($this->url) . '.mp3';
            if (!is_file($mp3filepath)) {
                $is_aliyun = true;
                if ($is_aliyun) {
                    $nowUrl = Alioss::instance()->getSignUrl($this->url);
                    $content = @file_get_contents($nowUrl);
                    $filepath = '/tmp/' . md5($nowUrl) . '.amr';
                    file_put_contents($filepath, $content);
                } else {
                    $filepath = $this->url;
                }
                exec('ffmpeg -i ' . $filepath . '  -ab 128 ' . $mp3filepath);
            }
            if (is_file($mp3filepath)) {
                header('Expires:Sun, 01 Mar 2015 11:40:14 GMT');
                header('ETag:10490094371019910446');
                header('Content-type: audio/mpeg');
                header("Accept-Ranges: bytes");
                $filesize = filesize($mp3filepath);
                header("Accept-Length: $filesize");
                readfile($mp3filepath);
            }