####################################################################################################
**资源列表**
####################################################################################################

******************************************************************************************
**后台前端资源列表**
******************************************************************************************

资源路径	备注
'/public/common/js/cc.js'	前端小框架
'/public/common/js/functions.js'	必备函数库
'/public/common/js/common.js'	必备函数库
'/public/plug/popup/popup.js'	弹窗
'/public/plug/tip/tip.js'	提示框
'/public/plug/tree/x-tree.js'	树
'/public/plug/DatePicker/WdatePicker.js'	日期选择器
'/public/common/js/jquery.min.js'	手撸DOM必备
'/public/plug/loading/loading.js'	加载图标
'/public/common/js/language/message.js'	翻译函数
'/public/common/css/base.css'	后台内置样式
'/public/common/css/layouts.css'	后台内置样式
'/public/common/css/adminComm.css'	后台内置样式
'/public/plug/icon/iconfont.css'	少切点图
'/public/plug/webupload/dist/webuploader.css'	文件上传
'/public/plug/webupload/dist/webuploader.min.js'	文件上传
'/public/plug/imgview/imgview.js'	图片查看器
'/public/plug/chart/echarts.min.js'	图表
'/public/plug/zclip/js/ZeroClipboard.min.js'	剪切板
'/public/plug/validator/validator.js'	校验器
'/public/plug/kindeditor/kindeditor-all-min.js'	富文本编辑器
'/public/plug/audio/soundmanager2-nodebug-jsmin.js'	
'/public/plug/select2/css/select2.min.css'	
'/public/plug/select2/js/select2.full.min.js'	
'/public/plug/tooltip/tooltip.css'	
'/public/plug/tooltip/tooltip.js'	

******************************************************************************************
**服务器本地路径**
******************************************************************************************

说明	代码	例子
根目录	realpath(\CC::app()->basePath . '/..');	/data/websites/deve2/zf.xbwq.com.cn/wq
protected	\CC::app()->basePath;	/data/websites/deve2/zf.xbwq.com.cn/wq/protected
public	realpath(\CC::app()->basePath . '/../public');	/data/websites/deve2/zf.xbwq.com.cn/wq/public
files	realpath(\CC::app()->basePath . '/../files');	/data/websites/deve2/zf.xbwq.com.cn/wq/files
导出路径(files/export/Ymd)	realpath(Excel::getBaseDir());	/data/websites/deve2/zf.xbwq.com.cn/wq/files/export/20181102
引入CC2框架的某个PHP文件	require_once CC_PATH . '/util/external/excel/Classes/PHPExcel.php';	

******************************************************************************************
**URL**
******************************************************************************************

说明	代码	例子
public URL	\CC::app()->getBaseUrl() . '/public'	/wq/public
协议://域名/项目根目录	\CC::app()->request->getHostInfo(true);	http://zfdeve2.xbwq.com.cn/wq
协议://域名	\CC::app()->request->getHostInfo(false);	http://zfdeve2.xbwq.com.cn


******************************************************************************************
**路径转换**
******************************************************************************************

说明	代码
URL转服务器本地路径	filePath=\CC::app()−>request−>getFilePath(
url);
服务器本地路径转URL	fileUrl=\CC::app()−>request−>getHostInfo(true).strreplace(\CC::app()−>basePath.′/..′,″,
filePath);

******************************************************************************************
**可用路径模板**
******************************************************************************************

说明	代码
excel导入错误原因	Excel::getBaseDir() . "/错误原因_" . uniqid() . '.xls';




