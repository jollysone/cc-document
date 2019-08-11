####################################################################################################
**Helper & Utils**
####################################################################################################

Helper & Utils




缓存

return Cache::instance()->getForCallback(CacheKey::getForClassKey('methodName'), function () {
               
});
CURL

$curl = Curl::instance();
$url = 'http://restapi.amap.com/v3/geocode/geo';
$params = [
    'key' => '3275d38f5e03c4c8a1451450207d54aa',
    'address' => '江苏省苏州市吴江区'
];
$result = $curl->get($url, $params);
$result = $curl->post($url, $params);
抛出异常

throw new \CErrorException('');
打印SQL

\CModel::getLastSql();
\CModel::debugSql();
\CModel::getAlllSql();
构造URL

\CC::app()->url->genurl($action_str, $params);
获取当前URL的分组

$group = \CC::app()->url->getGroup();
当前页面URL

\CC:app()->url->genurl('');
文件URL签名

FileUtil::getSignUrl();
文件URL反签名

FileUtil::aliyunUrlUnsigned();
取二维数组某一列数据

ArrayUtil::arrayColumn();
改二维数组的索引

ArrayUtil::arrayFillKey();
带分隔符的字符串转数组

ArrayUtil::explodeStr();
发IM

// $from，说明作用
// $to，用户id，起决定性作用
// $notice_type，文档约定
// $json，附加信息
// $online，0给所有人发，1只给在线的人发
IM::instance()->sendNotice($from, $to, $notice_type, $json, $online = 0,$noticesubtype = '0')
发邮件

Mail::sendMsg('aubert7@163.com', 'sender', 'title', 'body');
打印日志(项目根路径/protected/runtime)

\CC::log();
下载文件到当前服务器

//$filePath 项目根路径/files/Y/m/d/$file.ext
//$fileUrl http://域名/项目根目录名/files/Y/m/d/$file.ext
list($filePath, $fileUrl) = FileUtil::download($url, $file);
上传文件到阿里云

$alioss = Alioss::instance();
$aliyunFileUrl = $alioss->getPathForUrl($ourServerFileUrl, 'image/jpg', 0);
$alioss->uploadFile($outServerFilePath, $aliyunFileUrl);
$aliyunFileUrlWithoutSign = $aliyunFileUrl;
$aliyunFileUrlWithSign = $alioss->getSignUrl($aliyunFileUrl, true);
遍历目录

function traverse_dir($dir) {
    $files = [];
    if (@$handle = opendir($dir)) { //注意这里要加一个@，不然会有warning错误提示:)
        while (($file = readdir($handle)) !== false) {
            if ($file != ".." && $file != ".") { //排除根目录；
                if (is_dir($dir . "/" . $file)) { //如果是子文件夹，就递归
                    $files[$file] = traverse_dir($dir . "/" . $file);
                } else { //否则将文件的名字存入数组；
                    $files[] = $file;
                }
            }
        }
        closedir($handle);
    }
    return $files;
}




