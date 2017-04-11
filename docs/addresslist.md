# 通讯录服务接口定义  

----------

<h2 id="cid_0">查询部门通讯录</h2>  

<h3 id="cid_0_0">说明</h3>  

查询部门通讯录。    

<h3 id="cid_0_1">URL</h3>  

http://ip:port/addresslist/addrlist/getaddrlist.do?departmentid=1   

<h3 id="cid_0_2">HTTP请求方式</h3>  

GET  

<h3 id="cid_0_3">请求参数</h3>  

<table>
   <tr>
      <td>参数</td>
      <td>类型</td>
      <td>必选</td>
      <td>描述</td>
   </tr>
   <tr>
      <td>departmentid</td>
      <td>String</td>
      <td>是</td>
      <td>部门id</td>
   </tr>
</table>

<h3 id="cid_0_4">返回数据</h3> 

<table>
   <tr>
      <td>参数</td>
      <td>类型</td>
      <td>必选</td>
      <td>描述</td>
   </tr>
   <tr>
      <td>code</td>
      <td>String</td>
      <td>是</td>
      <td>结果码，【0：成功，其他见错误码定义】</td>
   </tr>
   <tr>
      <td>msg</td>
      <td>String</td>
      <td>否</td>
      <td>错误消息</td>
   </tr>
   <tr>
      <td>departments</td>
      <td colspan="3">部门集合</td>
   </tr>
   <tr>
      <td>department_id</td>
      <td>String</td>
      <td>是</td>
      <td>部门id</td>
   </tr>
   <tr>
      <td>department_name</td>
      <td>String</td>
      <td>是</td>
      <td>部门名称</td>
   </tr>
   <tr>
      <td>parent_department_id</td>
      <td>String</td>
      <td>是</td>
      <td>父部门id</td>
   </tr>
   <tr>
      <td>ec_id</td>
      <td>String</td>
      <td>是</td>
      <td>企业标识</td>
   </tr>
   <tr>
      <td>ldap_dnpath</td>
      <td>String</td>
      <td>否</td>
      <td>Ldap路径</td>
   </tr>
   <tr>
      <td>createtype</td>
      <td>String</td>
      <td>是</td>
      <td>创建类型</td>
   </tr>
   <tr>
      <td>subMembers</td>
      <td colspan="3">成员集合</td>
   </tr>
   <tr>
      <td>member_id</td>
      <td>String</td>
      <td>是</td>
      <td>成员id主键</td>
   </tr>
   <tr>
      <td>name</td>
      <td>String</td>
      <td>是</td>
      <td>成员名称</td>
   </tr>
   <tr>
      <td>account</td>
      <td>String</td>
      <td>是</td>
      <td>成员集合</td>
   </tr>
   <tr>
      <td>phone_num</td>
      <td>String</td>
      <td>是</td>
      <td>成员手机号码</td>
   </tr>
   <tr>
      <td>mail</td>
      <td>String</td>
      <td>是</td>
      <td>成员邮件</td>
   </tr>
   <tr>
      <td>job_position</td>
      <td>String</td>
      <td>是</td>
      <td>职位</td>
   </tr>
   <tr>
      <td>status</td>
      <td>String</td>
      <td>是</td>
      <td>成员状态 0：未知 1：已关注 2：冻结 4：未关注</td>
   </tr>
   <tr>
      <td>department_id</td>
      <td>String</td>
      <td>是</td>
      <td>部门id</td>
   </tr>
   <tr>
      <td>ec_id</td>
      <td>String</td>
      <td>是</td>
      <td>企业id</td>
   </tr>
   <tr>
      <td>createtype</td>
      <td>int</td>
      <td>是</td>
      <td>创建类型 1-页面创建 2-ldap同步</td>
   </tr>
   <tr>
      <td>im_user_id</td>
      <td>String</td>
      <td>是</td>
      <td>im账号</td>
   </tr>
   <tr>
      <td>im_sec</td>
      <td>String</td>
      <td>是</td>
      <td>im描述</td>
   </tr>
   <tr>
      <td>creat_datetime</td>
      <td>String </td>
      <td>是</td>
      <td>创建时间</td>
   </tr>
</table>  

响应体示例：  

```javascript
{
    "code": "0",
    "msg": "获取通讯录成功",
    "addressList": {
        "department": null,
        "subMembers": [
            {
                "member_id": "97192b82-2a9b-4b1a-a323-a107594e86dd",
                "name": "成少波",
                "account": "chengshaobo",
                "phone_num": "18061779660",
                "mail": "chengshaobo@nj.fiberhome.com.cn",
                "job_position": "",
                "status": "",
                "department_id": "1",
                "ec_id": "*",
                "createtype": "2",
                "im_user_id": "826",
                "im_sec": "25667b4917080c71ba215272d3db7cde",
                "creat_datetime": "2016-08-25 16:42:19.0"
            }
        ],
        "departments": [
            {
                "department_id": "9b192c83-02e5-43ee-88c9-31a4378875a0",
                "department_name": "开发一部一室",
                "parent_department_id": "1",
                "ec_id": "*",
                "ldap_dnpath": null,
                "createtype": 1
            },
            {
                "department_id": "8c25957e-99ea-46f1-97a6-8a0f02a9ebc6",
                "department_name": "开发一部二室",
                "parent_department_id": "1",
                "ec_id": "*",
                "ldap_dnpath": null,
                "createtype": 1
            },
            {
                "department_id": "54b5f449-2803-49f3-a68e-f0ef4e6812cc",
                "department_name": "开发一部三室",
                "parent_department_id": "1",
                "ec_id": "*",
                "ldap_dnpath": null,
                "createtype": 1
            }
        ]
    }
}
```  

<h2 id="cid_1">查询用户信息 </h2>  

<h3 id="cid_1_0">说明</h3>  

查询用户信息。    

<h3 id="cid_1_1">URL</h3>  

http://ip:port/addresslist/userInfo/getUserInfo.do?userId=xxx    

<h3 id="cid_1_2">HTTP请求方式</h3>  

GET  

<h3 id="cid_1_3">请求参数</h3>  

<table>
   <tr>
      <td>参数</td>
      <td>类型</td>
      <td>必选</td>
      <td>描述</td>
   </tr>
   <tr>
      <td>userId</td>
      <td>String</td>
      <td>是</td>
      <td> im账号</td>
   </tr>
</table>

<h3 id="cid_1_4">返回数据</h3>  

<table>
   <tr>
      <td>参数</td>
      <td>类型</td>
      <td>必选</td>
      <td>描述</td>
   </tr>
   <tr>
      <td>code</td>
      <td>String</td>
      <td>是</td>
      <td>结果码，【0：成功，10000：userId值为空，10001：userId不存在】</td>
   </tr>
   <tr>
      <td>msg</td>
      <td>String</td>
      <td>否</td>
      <td>错误信息</td>
   </tr>
   <tr>
      <td>member_id</td>
      <td>String</td>
      <td>是</td>
      <td>成员id</td>
   </tr>
   <tr>
      <td>name</td>
      <td>String</td>
      <td>是</td>
      <td>成员名称</td>
   </tr>
   <tr>
      <td>account</td>
      <td>String</td>
      <td>是</td>
      <td>成员账号</td>
   </tr>
   <tr>
      <td>phone_num</td>
      <td>String</td>
      <td>是</td>
      <td>手机号码</td>
   </tr>
   <tr>
      <td>mail</td>
      <td>String</td>
      <td>是</td>
      <td>邮箱</td>
   </tr>
   <tr>
      <td>job_position</td>
      <td>String</td>
      <td>是</td>
      <td>职位</td>
   </tr>
   <tr>
      <td>status</td>
      <td>String</td>
      <td>是</td>
      <td>成员状态 0：未知 1：已关注 2：冻结 4：未关注</td>
   </tr>
   <tr>
      <td>department_id</td>
      <td>String</td>
      <td>是</td>
      <td>部门id</td>
   </tr>
   <tr>
      <td>department_name</td>
      <td>String</td>
      <td>是</td>
      <td>部门名称</td>
   </tr>
   <tr>
      <td>ec_id</td>
      <td>String</td>
      <td>是</td>
      <td>企业id</td>
   </tr>
   <tr>
      <td>createtype</td>
      <td>String</td>
      <td>是</td>
      <td>创建类型 1-页面创建 2-ldap同步</td>
   </tr>
   <tr>
      <td>im_user_id</td>
      <td>String</td>
      <td>是</td>
      <td>im账号</td>
   </tr>
   <tr>
      <td>im_sec</td>
      <td>String</td>
      <td>是</td>
      <td>im描述</td>
   </tr>
   <tr>
      <td>creat_datetime</td>
      <td>String</td>
      <td>是</td>
      <td>创建时间</td>
   </tr>
</table>  

响应体示例：  

```javascript
{
    "code": "0",
    "msg": "成功",
    "imUser": {
         "member_id": "97192b82-2a9b-4b1a-a323-a107594e86dd",
         "name": "张三",
         "account": "zhangsan",
         "phone_num": "13111111111",
         "mail": "zhangsan@nj.fiberhome.com.cn",
         "job_position": "",
         "status": "",
         "department_id": "1",
         "department_name": "产品部",
         "ec_id": "*",
         "createtype": "2",
         "im_user_id": "826",
         "im_sec": "25667b4917080c71ba215272d3db7cde",
         "creat_datetime": "2016-08-25 16:42:19.0"
    }
}
```  

<h2 id="cid_2">客户端上传头像</h2>  

<h3 id="cid_2_0">说明</h3>  

客户端上传头像。  

<h3 id="cid_2_1">URL</h3>  

http://ip:port/addresslist/userFavicon/uploadUserFavicon.do   

<h3 id="cid_2_2">HTTP请求方式</h3>  

POST  

<h3 id="cid_2_3">请求参数</h3>  

<table>
   <tr>
      <td>参数</td>
      <td>类型</td>
      <td>必选</td>
      <td>描述</td>
   </tr>
   <tr>
      <td>userId</td>
      <td>String</td>
      <td>是</td>
      <td>im的id</td>
   </tr>
   <tr>
      <td>file</td>
      <td>String</td>
      <td>是</td>
      <td>头像图片体</td>
   </tr>
</table>

<h3 id="cid_2_4">返回数据</h3>  

<table>
   <tr>
      <td>参数</td>
      <td>类型</td>
      <td>必选</td>
      <td>描述</td>
   </tr>
   <tr>
      <td>resultCode</td>
      <td>String</td>
      <td>是</td>
      <td>0:成功  10000:账号ID为空 10001:账号ID不存在 10003:file为空</td>
   </tr>
   <tr>
      <td>resultMsg</td>
      <td>String</td>
      <td>否</td>
      <td>信息</td>
   </tr>
</table>  

响应体示例：  

```javascript
{
    "resultCode": "0",
    "resultMsg": "上传成功"
}
```  

<h2 id="cid_3">客户端下载头像</h2>  

<h3 id="cid_3_0">说明</h3>  

客户端下载头像。  

<h3 id="cid_3_1">URL</h3>  

http://ip:port/addresslist/userFavicon/downloadUserFavicon.do?userId=xxx     

<h3 id="cid_3_2">HTTP请求方式</h3>  

GET  

<h3 id="cid_3_3">请求参数</h3>  

<table>
   <tr>
      <td>参数</td>
      <td>类型</td>
      <td>必选</td>
      <td>描述</td>
   </tr>
   <tr>
      <td>userId</td>
      <td>String</td>
      <td>是</td>
      <td>im的id</td>
   </tr>
</table>

<h3 id="cid_3_4">返回数据</h3>  

图片字节流

