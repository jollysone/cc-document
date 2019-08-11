####################################################################################################
**基本控制器**
####################################################################################################

******************************************************************************************
**校验器**
******************************************************************************************

checkers 最大长度

$arr = [['len', 'max' => 100]];
checkers 必填

$arr = [['must']];
checkers 数字

$arr = [['int']];
多个checker的配置

array_merge(['must'], [['len', 'max' => 40]])



******************************************************************************************
**CAction**
******************************************************************************************

如果只需简单的处理数据功能, 可以直接继承 ``\CAction`` 并重写 ``execute(CRequest $request)`` 方法则可以实现功能。

重写后返回值需是一个 ``Response`` 响应, 这部分可参考 ``响应(Response)`` 章节。

.. code-block:: php
    :linenos:
    :emphasize-lines: 2,4,10-12

    <?php
        class ExampleApiAction extends \CAction
        {
            public function execute(CRequest $request)
            {
                ...

                ...
                
                return new CJsonData([
                    'result' => 'success'
                ]);
            }

        }
    ?>



分组

//是action的基础, 特别重要
public function supportGroups() {    
    return 'api,admin';
}
执行一个action

$req = new CRequest();
$req->putParams('','');
$action = new CityIndexCaseCmdAction();
$action->init();
$ret = $action->execute($req);
$ret = $ret->getData();
校验器

protected function getCheckers() {    
    return array_merge(CheckCreator::create($this), []);
}
面包屑

protected function getBreadcrumbs() {    
    return [        
        ['name' => ''],        
        ['name' => '',  'url' => $this->genurl()]
    ];
}
标题

public function getPageTitle() { 
    return $this->pageTitle;
}
<title><?php echo $this->pageTitle ;?></title>
开启事务

protected function getIsOpenTransaction() {    
    return true;
}
配置布局文件

public function getLayouts() {
    return '/layouts/default';
}







******************************************************************************************
**ListAction**
******************************************************************************************

如果是一个列表页则可以继承这个方法。

基本的 ListAction 所需要的。

1. 重写获得表名方法确认操作哪个数据表。
2. 重写搜索条件方法, 查询出想要的数据, 同时也是配合顶部搜索项。
3. 在显示列表前预处理数据

一般都是还实现了后台列表, 所以还需实现三个方法。

1. 创建数据过滤器。
2. 创建列表的字段。
3. 创建列表数据条的操作按钮。



.. code-block:: php
    :linenos:
    :emphasize-lines: 2

    <?php
        class ExampleApiAction extends ListAction implements ITableViewCreator
        {
            protected function getTable()
            {
                return DBUtils::COLLECT_TASK_HANDLE_DETAIL; // 返回表名
            }

            protected function getSearchCondition()
            {
                $this->dbCondition->leftJoin(DBUtils::COLLECT_TASK_USER, 'task_user', 't.id = task_user.work_id');

                ...

                $this->dbCondition->group('t.id')
                    ->order('t.is_draft desc, t.submit_time desc')
                    ->select('t.*');

            }

            protected function onListBefore(&$list)
            {
                return [
                    new WorkListBeforeAdminHandler(), // 主办人协办人处理
                ];
            }


            public function createListFilters()
            {
                $filters[] = (new SelectFilter('case_type', '案事件类型', $this->case_type_list, 'drop-pop'))->setIsMultiple(false);
                $filters[] = (new SelectFilter('case_source', '案事件来源', $this->case_source_list, 'drop-pop'))->setIsMultiple(false);
                $filters[] = (new SelectFilter('case_attribute', '案事件性质', $this->case_attribute_list, 'drop-pop'))->setIsMultiple(false);
            
                return $filters;
            }

            public function createListColumns(array $list)
            {
                $columns[] = new Column('状态', 'status', function ($data){
                    if ($data['status'] == TaskOpTypeEnum::TRANS){
                        return TaskOpTypeEnum::HANDLE_STATUS[TaskOpTypeEnum::DONE];
                    }else{
                        return TaskOpTypeEnum::HANDLE_STATUS[$data['status']];
                    }
                });

                $columns[] = new Column('提交人', 'uploader_name');
                $columns[] = new Column('结案时间', 'upload_time', function ($data){
                    if ($data['status'] == TaskOpTypeEnum::ING){
                        return '';
                    }else{
                        return date('Y-m-d H:i',$data['upload_time']);
                    }

                });
                
                return $columns;
            }

            public function createOperateButtons(array $list)
            {
                return [
                    function ($data) {
                        if ($data['is_draft'] == 1){
                            $buttons[] = new OperateButtonWidget('删除','draftdelete', ['is_task' => 0]);
                        }else{
                            if (AuthManager::instance()->checkAuth(ZhifaAuth::ENFORCEMENT_DELETE)){
                                $buttons[] = (new OperateButtonWidget('删除','workdelete',[],'','',[
                                    'success-after' => 'add_success'
                                ]))->addClassnames('btn-danger');
                            }
                        }

                        if (is_array($buttons)){
                            return new ArrayDataWidget($buttons);
                        }else{
                            return [];
                        }

                    }
                ];
            }
        }
    ?>





分页器

//数据总量
$this->getPage()->count;

//取分页器
$this->getPage();

//自定义分页大小
echo WidgetBuilder::build(
    new ListTableWidget($this, $list, $page, ['is_show_sequence' => true, 'is_show_page_num' => true]), 
    ListTablePanel::instance()
);
配置ListAction返回的数据格式

protected function getDataType() {        
    return 'json';    
}
表名

protected function getTable() {    
    return '';
}
用于给API附加字段、或给视图文件附加变量

protected function onExecute() {    
    return [        
        'field' => $value    
    ]
}
只查询一条数据

protected function getIsSingle() {    
    return true;
}
查询条件

protected function getSearchCondition() {    
    $this->dbCondition->addId($id);    
    $this->dbCondition->addColumn($field, $value)    
    $this->dbCondition->addStrCondition();    
    $this->dbCondition->addColumnsCondition([])    
    $thid->dbCondition->addConditions([])
}
开启ListAction导出功能

 public $is_export;
 
 protected function isExport() {    
    return $this->is_export;
 }
 
 protected function onExecExport($list) {    
    $excel_data = ExcelBuilder::build($this, $list);    
    return Excel::instance($excel_data)
        ->setExportDirForFlag()
        ->createExeclForDown('xx', 'xx.zip');
 }
导出图片的Column配置

list($filename, $url) = Excel::instance(ExcelBuilder::build($this, $list))
    ->setExportDirForFlag()
    ->createExeclForSave('');

$columns[] = (new Column('', 'pic'))->setExcelValueSetter(function ($data) {
    return new FileDownColumnValueSetter('pic', 'images/' . $data['id']);
});
如何关闭分页

public function getPageSize() {    
    return 0;
}
ITableViewCreator 配置过滤器

public function createListFilters() { 
    $filters[] = new Filter(); 
    return filters;
}
ITableViewCreator 配置数据列

public function createListColumns(array $list) {    
    $columns[] = new Column($title, $field, $valueSetter);    
    return columns;
}
ITableViewCreator 配置操作按钮

public function createOperateButtons(array $list) {    
    $buttons[] = new Button();    
    return $buttons;
}
使用每一行对应的$data来配置操作按钮

public function createOperateButtons(array $list) {    
    return [function ($data) {
        $buttons = [];
        return new ArrayDataWidget($buttons);
        
    }];
}
切换数据库

protected function getListModel()
{
    $model = parent::getListModel();
    $model->setDbConnectListener();
    return $model;
}
是否使用布局文件

//弹窗不卡的秘密哦
public function getIsLayout() {
    return false;
}
布局文件配置

public function getLayouts() {
    return '/layouts/default';
}








******************************************************************************************
**DetailAction**
******************************************************************************************

DetailAction extends ListAction

******************************************************************************************
**SaveAction**
******************************************************************************************

表名

protected function getTable() {    
    return '';
}
新增还是编辑

$this->idAdd();
处理哪些提交的数据

protected function getPostNames() {    
    return PostNamesCreator::create($this);
}
当前提交的字段在存数据库之前

protected function onBeforeSave(&$data) {    
    return [        
        new TimeCreateEditSaveBeforeHandler('c_time')    
    ];
}
当前提交的字段在存数据库之后

protected function onAfterSave($data) {    
    
}
获取当前详情数据

protected function getDetData() {    
    $data  = parent::getDetData();    
    $data['field'] = 'value';    
    return $data;
}
IFormViewBuilder 配置表单的输入框

public function createFormInputs() {    
    $inputs = [];    
    $inputs[] = new Input();    
    return $inputs;
}
存储完数据后自动跳转的链接

protected function getSaveRedirectUrl($data) {
    return $this->genurl('save');
}






******************************************************************************************
**DeleteAction**
******************************************************************************************

DeleteAction







给$list附加新字段

一对一

//关联表关联字段默认是id
AdditionDataListBeforeHandler('关联表名', '本表关联字段', ['新字段名' => '关联表字段']);

AdditionDataList::instance('关联表名', '本表关联字段', ['新字段名' => '关联表字段'])->additionData($list);
一对多

AdditionDataList::instance('关联表名', '关联表关联字段', ['新字段名' => [
    '新字段1' => '关联表字段1', 
    '新字段2' => '关联表字段2'
]], true, '本表关联字段(默认是id)')->additionData($list);

// 例子
AdditionDataList::instance('schema_data',  'schema_id', ['content' => [
    'id' => 'id', 
    'name' => 'val']], true)->additionData($schema_list);