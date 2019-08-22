####################################################################################################
**权限相关**
####################################################################################################

******************************************************************************************
**111**
******************************************************************************************

当前公司，是上级公司

CompanyServer::isManager()
当前公司，是村级公司

CompanyServer::isCun()
当前公司，是顶级公司

CompanyServer::isDing()
当前公司及其子公司的id列表

CompanyServer::getIds()
当前公司的子公司的id列表

CompanyServer::getSubComIds()
当前公司整个公司体系的 id列表

CompanyServer::getIds(CompanyServer::getRootId());
顶级公司id

CompanyServer::getRootId()
当前公司id

Session::getComID()
当前用户id

Session::getUserID()

SessionAbs::getUserClassify() == UserClassifyEnum::ADMIN








这些人，是否有某种权限？

AuthRange::getAuth(AuthType::getAuthType($authTypeString))->checkUids($uids)
当前这个人的某种权限，是哪种取值？

$authTypeString = AuthManager::AUTH_HOUSEHOLD_VIEW;
$int = AuthType::getAuthType($authTypeString)->getInt();
值	枚举	说明
0	AuthRangeNumEnum::NONE	没有权限
1	AuthRangeNumEnum::ALL	本公司
2	AuthRangeNumEnum::SUB	下属
3	AuthRangeNumEnum::ME	自己
4	AuthRangeNumEnum::CUSTOM	自定义
5	AuthRangeNumEnum::DEPT_SUB	本部门及下属部门
6	AuthRangeNumEnum::COMPANY_SUB	本公司及下级公司
某权限，对应的所有人

$uids = AuthRange::getAuth(AuthType::getAuthType($authTypeString))->getAllUids();
    
$uids = DiCreate::getAuthRangeNumEnum()->getRangeByAuthType(AuthType::getAuthType($authTypeString))->getAllUids();





