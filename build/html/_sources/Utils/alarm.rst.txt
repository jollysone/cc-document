####################################################################################################
**警信**
####################################################################################################

******************************************************************************************
**Notice消息**
******************************************************************************************

**方法：** **sendNotice(** $from, $to, $content, $noticetype, $online = 0, $noticesubtype = '0' **)**

**参数：** 

    **$from：** 发送者 `uid` , 填写 `admin` 则为管理员发送，

    **$to：** 接受者 `uids` 字符串, 例：'5' 或 '23,2,87,15'，

    **$content：** 发送内容（如需JSON格式需要自己转），

    **$noticetype：** 文档约定（与接收端约定），

    **$online：** 默认发给 `$to` 中所有人, 配置 ``$online = 1`` 只发给在线的用户，

    **$noticesubtype：** 文档子类型约定（与接收端约定）。

**返回：** **bool**

.. code-block:: php
    :linenos:

    <?php
        $result = IM::instance()->sendNotice('5', '23,2,87', json_encode([
            'task_id' => 502,
            'status' => 1
        ]), 'task_status_notice');
    ?>


******************************************************************************************
**Message消息**
******************************************************************************************

**方法：** **messages(** $sender, $content, $users, $isall = false **)**

**参数：** 

    **$sender：** 发送者 `uid` , 填写 `admin` 则为管理员发送，

    **$content：** 发送内容（如需JSON格式需要自己转），

    **$users：** 接受者 `uids` 数组, 例：['23', '2', '87', '15']，

    **$isall：** 文档约定（与接收端约定）。

**返回：** **bool**

.. code-block:: php
    :linenos:

    <?php
        // 发送给一个人
        $result = IM::instance()->messages('5', '内容', ['23', '7', '9']);

        // 发送给所有人 标记: $params['subtype'] = 'allusers';
        $result = IM::instance()->messages('5', '内容', ['23', '7', '9'], true);
    ?>


******************************************************************************************
**自定义消息**
******************************************************************************************

**方法：** **sendCustom(** $type, $from, $to, $json, $subtype = '', $agree = 1, $detail = '', $newapi = 1 **)**

**参数：** 

    **$type：** 文档约定（与接收端约定）'notice'、'message'、'business'、'update'，

    **$from：** 发送者 `uid` , 填写 `admin` 则为管理员发送，

    **$to：** 接受者 `uids` ，

    **$json：** 发送内容（如需JSON格式需要自己转），

    **$subtype：** 文档约定（与接收端约定），

    **$agree：** 是否同意，

    **$detail：** 详情，

    **$newapi：** 是否新API。

**返回：** **bool**

.. code-block:: php
    :linenos:
    :emphasize-lines: 3-12

    <?php
        public function sendCustom($type, $from, $to, $json, $subtype, $agree, $detail, $newapi){
            $rst = $this->request(array(
                'type' => $type,
                'from' => $from,
                'to' => $to,
                'subtype' => $subtype,
                'agree' => $agree,
                'detail' => $detail,
                'json' => $json,
                'newapi' => $newapi,
            ));

            return array($this->isOk($rst), $rst);
        }

        protected function request($params)
        {
            $params['secret'] = $this->_secret;
            $result = '';
            if ($this->is_request) {
                $result = Curl::instance()->post($this->_urlPrefix, $params);
            }
            $this->_requestInfo = 'url: ' . $this->_urlPrefix . '?' . http_build_query($params) . "<br>\n" . 'result: ' . $result;

            return $result;
        }
    ?>
