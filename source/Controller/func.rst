####################################################################################################
**控制器方法列表**
####################################################################################################

================================================================================
**配置操作表**
================================================================================

**适用：** ``ListAction`` ``DetailAction`` ``SaveAction`` ``DeleteAction``

**说明：** 需要对哪个表操作，就配置上对应的表即可。 

    - **注意1：** 通过 `CAction` 衍生的控制器都 **需要** 配置此项。

    - **注意2：** 返回表名 **一定要** 用 **宏定义/枚举值** 的方式。

**例1：** 配置控制器默认操作 'user' 表。

    .. code-block:: php
        :linenos:

        <?php
            protected function getTable()
            {111
                return DBUtils::USER;
            }
        ?>

================================================================================
**数据搜索条件**
================================================================================

**适用：** ``ListAction`` ``DetailAction``

**说明：** 配置搜索条件，具体可配置方法可参考 **数据库 -> 基本使用方法-> 条件控制** 。

    - **列表页：** 一般根据条件重写此方法，同时也是联动筛选项的，

    - **详情页：** 一般不需重写，默认自动获取 **id** 关联表条件。

**例1：** 列表页重写搜索条件。

    .. code-block:: php
        :linenos:

        <?php
            protected function getSearchCondition()
            {
                $this->dbCondition->leftJoin(DBUtils::USER, 'u', 't.id = u.work_id');

                ...

                $this->dbCondition->group('t.id')
                    ->order('t.is_draft desc, t.submit_time desc')
                    ->select('t.*');

            }
        ?>

**例2：** 详情页通过类属性反射自动获取到 **id** 并自动添加条件。

    .. code-block:: php
        :linenos:

        <?php
            $this->dbCondition->addColumnsCondition(array(
                't.id' => $this->id,
            ));
        ?>

================================================================================
**预处理数据**
================================================================================

**适用：** ``ListAction`` ``DetailAction``

**说明：** 如果有需要预处理的数据，把预处理逻辑写在 **beforHandler** 中处理显示前的数据即可。详细写法参考 **控制器 -> 流程处理器 -> listHandler** 。

    - **提示：** 以数组形式可返回多个流程处理器对象，执行顺序按索引顺序依次往后。

**例1：** 注入一个流程处理器对象 **ExampleListBeforeAdminHandler()** 。

    .. code-block:: php
        :linenos:

        <?php
            protected function onListBefore(&$list)
            {
                return [
                    new ExampleListBeforeAdminHandler(),
                ];
            }
        ?>

================================================================================
**配置表格字段**
================================================================================

**适用：** ``ListAction``

**说明：** 可以配置列表页所需显示的字段，详细用法可见 **视图组件 -> 列表 -> 配置表格字段** 。

    - **注意：** 需要实现 ``ITableViewCreator`` 才可以使用此方法。

**例1：** 配置列表名为 **标题** 的一列。

    .. code-block:: php
        :linenos:

        <?php
            public function createListColumns(array $list)
            {
                $columns[] = new Column('标题', 'title');

                return $columns;
            }
        ?>

================================================================================
**配置操作按钮**
================================================================================

**适用：** ``ListAction``

**说明：** 可以配置列表页列表后面的操作按钮，详细用法可见 **视图组件 -> 列表 -> 配置操作按钮** 。

    - **注意：** 需要实现 ``ITableViewCreator`` 才可以使用此方法。

**例1：** 在列表中配置 ``详情`` 、``编辑`` 和 ``删除`` 三个按钮。

    .. code-block:: php
        :linenos:

        <?php
            public function createOperateButtons(array $list)
            {
                return [
                    function ($data) {
                        $buttons[] = new ViewButtonWidget('详情', 'detail');
                        $buttons[] = new EditAjaxButtonWidget('编辑', 'edit');
                        $buttons[] = new OperateButtonWidget('删除','delete');

                        return new ArrayDataWidget($buttons);
                    }
                ];
            }
        ?>

================================================================================
**配置面包屑**
================================================================================

**适用：** ``ListAction``

**说明：** 可以配置列表页顶部的面包屑显示。

**例1：** 

    .. code-block:: php
        :linenos:

        <?php
        protected function getBreadcrumbs() {    
                return [        
                    ['name' => ''],        
                    ['name' => '',  'url' => $this->genurl()]
                ];
            }
        ?>


================================================================================
**配置过滤器**
================================================================================

**适用：** ``ListAction``

**说明：** 可以配置列表页顶部的过滤器显示，详细用法可见 **视图组件 -> 过滤器** 。

    - **注意：** 需要实现 ``ITableViewCreator`` 才可以使用此方法。

**例1：** 配置列表页顶部的过滤器：**时间搜索** 和 **状态筛选** 。

    .. code-block:: php
        :linenos:

        <?php
            public function createListFilters()
            {
                $filters[] = new TimeRangeFilter('time', '时间', 'simple');
                $filters[] = new SelectFilter('sub_status', '状态', TaskOpTypeEnum::getValues());

                return $filters;
            }
        ?>

================================================================================
**访问支持分组**
================================================================================

**适用：** ``CAction`` ``ListAction`` ``DetailAction`` ``SaveAction`` ``DeleteAction``

**说明：** 可以重写支持固定的分组，默认不写就是全部都能够访问（ **return '_all'** ），支持分组详见 **架构 -> 模块设计 -> 路由分组模块设计** 。

**例1：** 配置支持 ``api`` 和 ``admin`` 分组访问。

    .. code-block:: php
        :linenos:

        <?php
            public function supportGroups() {    
                return 'api,admin';
            }
        ?>

================================================================================
**获得网页标题**
================================================================================

**适用：** ``CAction`` ``ListAction`` ``DetailAction`` ``SaveAction`` ``DeleteAction``

**说明：** 此方法可以获得网页标题信息，如需修改可重写 ``$this->pageTitle`` 属性即可。

**例1：** 获得网页标题信息。

    .. code-block:: php
        :linenos:

        <?php
            public function getPageTitle() { 
                return $this->pageTitle;
            }
        ?>

================================================================================
**开启控制器事务**
================================================================================

**适用：** ``CAction`` ``ListAction`` ``DetailAction`` ``SaveAction`` ``DeleteAction``

**说明：** 重写此方法返回 ``true`` 即可打开控制器事务开关。

**例1：** 获得网页标题信息。

    .. code-block:: php
        :linenos:

        <?php
            protected function getIsOpenTransaction() {    
                return true;
            }
        ?>

================================================================================
**配置布局文件**
================================================================================

**适用：** ``CAction`` ``ListAction`` ``DetailAction`` ``SaveAction`` ``DeleteAction``

**说明：** 重写属性 ``$layouts`` 配置布局文件模板。默认是 ``模板1``, 只显示视图组件的可配置 ``模板2`` ，一般不需要显示页面组件的可配置 ``模板3`` 进行隐藏。

    - **模板1：** '/layouts/default'：是包括了整个管理端页面的模板。 **默认是这个模板** 。

    - **模板2：** '/layouts/simple'：只渲染视图组件的模板。

    - **模板3：** false：不渲染模板。

**提示：** 页面上是否有视图组件取决于是否实现 ``ITableViewCreator`` 。

**例1：** 底层默认获取视图布局模板。

    .. code-block:: php
        :linenos:

        <?php
            public function getLayouts() {
                return $this->layouts;
            }
        ?>

**例2：** 修改模板，让网页只渲染视图组件的模板。

    .. code-block:: php
        :linenos:

        <?php
            public $layouts = '/layouts/simple';
        ?>


================================================================================
**是否使用布局文件**
================================================================================

**适用：** ``ListAction`` ``DetailAction`` ``SaveAction`` ``DeleteAction``

**说明：** 重写 ``getIsLayout()`` 方法配置不加载布局配置模板。（默认不重写是 **true** ）

    - **提示：** 适合只写了相关内容而不需要加载布局配置模板的控制器。

**例1：** 配置不加载布局配置模板。

    .. code-block:: php
        :linenos:

        <?php
            // 弹窗不卡的秘密哦
            public function getIsLayout() {
                return false;
            }
        ?>
 
================================================================================
**配置控制器返回的数据格式**
================================================================================

**适用：** ``ListAction`` ``DetailAction``

**说明：** 重写 ``getDataType()`` 方法配置配置控制器返回的数据格式。（默认不重写是 **'render'** 方式）

    - **提示：** 适合既想继承 ``ListAction`` 或 ``DetailAction`` 控制器，又不想返回页面响应格式的情况。

**例1：** 配置不加载布局配置模板。

    .. code-block:: php
        :linenos:

        <?php
            protected function getDataType() {        
                return 'json';    
            }
        ?>

**底层实现：** 通过配置不同的 **$data_type** 来实现不同的响应方式。

    .. code-block:: php
        :linenos:

        <?php
            switch ($data_type) {
                case 'json':
                    return new CJsonData($data);
                case 'jsonp':
                    return new CJsonpData($data);
                case 'render':
                    return new CRenderData($data, $view, $isLayout, $layouts, $view_dir);
                default:
                    return new CNoneData($data);
            }
        ?>

================================================================================
**返回响应附加字段**
================================================================================

**适用：** ``ListAction`` ``DetailAction`` ``SaveAction`` ``DeleteAction``

**说明：** 重写 ``onExecute()`` 方法返回一个数组，添加需要附加的字段即会在输出 **Response** 响应合并输出数据。

**例1：** 在返回的数据中追加总条数字段。

    .. code-block:: php
        :linenos:

        <?php
            protected function onExecute()
            {    
                return [        
                    'total' => CDbCommand::count($this->dbCondition)    
                ]
            }
        ?>

**底层实现：** 通过合并方式追加在里面。

    .. code-block:: php
        :linenos:

        <?php
            array_merge($data, $this->onExecute())
        ?>

================================================================================
**开启导出功能**
================================================================================

**适用：** ``ListAction``

**说明：** 只适合列表页控制器开启导出功能（默认配置是 **false** ）。文件导出方法详见： **文件系统 -> 导出文件** 。

    - **提示：** 判断是命令行环境执行即为导出，就会执行 ``onExecExport($list)`` 方法把数据导出。

**例1：** 

    .. code-block:: php
        :linenos:
        :emphasize-lines: 3,12

        <?php
            protected function isExport() {    
                return \CC::app()->url->getGroup() == \CEnv::RUN_CMD;
            }

            protected function onExecExport($list) {    
                $excel_data = ExcelBuilder::build($this, $list, [
                    new CustomFieldColumnBuildBeforeHandler('xxx', ['is_export_field' => true])
                ]);
                FileExportServer::asyncExportExcel($excel_data, 'xxx导出表', false);

                return new \CNoneData();
            }
        ?>


================================================================================
**配置导出图片**
================================================================================

**适用：** ``ListAction``

**说明：** 列表控制器导出列项有图片。文件导出方法详见： **文件系统 -> 导出文件** 。

**例1：** 

    .. code-block:: php
        :linenos:

        <?php



            尚未完善用法



            list($filename, $url) = Excel::instance(ExcelBuilder::build($this, $list))
                ->setExportDirForFlag()
                ->createExeclForSave('');

            $columns[] = (new Column('', 'pic'))->setExcelValueSetter(function ($data) {
                return new FileDownColumnValueSetter('pic', 'images/' . $data['id']);
            });
        ?>
 
================================================================================
**如何关闭分页**
================================================================================

**适用：** ``ListAction``

**说明：** 列表控制器关闭分页的显示。

**例1：** 

    .. code-block:: php
        :linenos:

        <?php
            public function getPageSize() {    
                return 0;
            }
        ?>
 

