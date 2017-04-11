# ExMobi-server6.x平台接口定义

----------

客户端跟服务器之间基于HTTP协议通讯，每个请求均定义了正常的响应消息，如果服务端处理完成后需要返回非正常消息，则返回FAULT响应消息。正常的响应消息HTTP状态码为200，FAULT响应消息HTTP状态码为412或500（详细说明请见“业务应答：FAULT”），客户端发出的HTTP请求头可分为通用头和业务HTTP头，业务HTTP头看具体接口定义章节。 

<h2 id="cid_0">HTTP通用头</h2>  

<h3 id="cid_0_0">定义</h3>  

请求头（表中蓝色字体部分为标准HTTP头，黑色字体为自定义通用头）  

<table>
   <tr>
      <td>名称</td>
      <td>类型</td>
      <td>值</td>
   </tr>
   <tr>
      <td><font color="blue">Host</font></td>
      <td><font color="blue">字符串</font></td>
      <td><font color="blue">主机地址，如：172.20.4.41:8001</font></td>
   </tr>
   <tr>
      <td><font color="blue">Connection</font></td>
      <td><font color="blue">字符串</font></td>
      <td><font color="blue">连接处理方式，固定值，值为keep-alive</font></td>
   </tr>
   <tr>
      <td><font color="blue">Accept-Encoding</font></td>
      <td><font color="blue">字符串</font></td>
      <td><font color="blue">接受的内容编码方式，固定值，值为gzip</font></td>
   </tr>
   <tr>
      <td><font color="blue">Accept-Language</font></td>
      <td><font color="blue">字符串</font></td>
      <td><font color="blue">支持的语言，如zh_CN，en_US，zh_TW，en_UK等</font></td>
   </tr>
   <tr>
      <td><font color="blue">Cookie</font></td>
      <td><font color="blue">字符串</font></td>
      <td><font color="blue">客户端会话标识，客户端首次请求时没有。格式：JSESSIONID=终端会话标识；例如JSESSIONID=4D4612C2CA19BC5DDC33F934A19BCE0B</font></td>
   </tr>
   <tr>
      <td><font color="blue">User-Agent</font></td>
      <td><font color="blue">字符串</font></td>
      <td><font color="blue">在原有头信息之后，添加： 空格 GAEA-Client，例如：User-Agent: Mozilla/5.0 (Linux; U; Android 5.0.0; zh-cn; GT-I9100 Build/GINGERBREAD) ,GAEA-Client</font></td>
   </tr>
   <tr>
      <td>imsi</td>
      <td>字符串</td>
      <td>IMSI号码（卡号），详情请参看“IMSI定义”章节。</td>
   </tr>
   <tr>
      <td>esn</td>
      <td>字符串</td>
      <td>ESN/IMEI号码（设备号），详情请参看“ESN定义”章节。</td>
   </tr>
   <tr>
      <td>pin</td>
      <td>字符串</td>
      <td>其值为黑莓pin码或iPhone/iPad/iPod/的devicetoken码。</td>
   </tr>
   <tr>
      <td>msisdn</td>
      <td>字符串</td>
      <td>手机号码，详情请参看“MSISDN定义”章节。</td>
   </tr>
   <tr>
      <td>ec</td>
      <td>字符串</td>
      <td>企业标识。客户端发送时需要在ec前加上$，标识其值已被Base64-UTF-8编码。</td>
   </tr>
   <tr>
      <td>encec</td>
      <td>字符串</td>
      <td>取值同$ec</td>
   </tr>
   <tr>
      <td>name</td>
      <td>字符串</td>
      <td>姓名（最大40字符），需要作Base64-UTF-8编码，客户端发送时需要在name前加上$，标识其值已被Base64-UTF-8编码，详情请参看“NAME定义”章节。</td>
   </tr>
   <tr>
      <td>encname</td>
      <td>字符串</td>
      <td>取值同$name</td>
   </tr>
   <tr>
      <td>os</td>
      <td>字符串</td>
      <td>操作系统；Android系统返回android；IOS系统返回ios；</td>
   </tr>
   <tr>
      <td>osversion</td>
      <td>字符串</td>
      <td>操作系统版本号，如1.5,2.0,2.2, 2.0 update1，pc固定为1.0，其他终端按照实际获取。</td>
   </tr>
   <tr>
      <td>platformid</td>
      <td>字符串</td>
      <td>手机型号，全小写；例：milestone、ipad、iphone、xt800</td>
   </tr>
   <tr>
      <td>appidentifier</td>
      <td>字符串</td>
      <td>应用的唯一标识；Android应用是应用的包名；Ios应用是应用的Bundle identifier</td>
   </tr>
   <tr>
      <td>clientversion</td>
      <td>字符串</td>
      <td>客户端版本号；例：3.1.0.0</td>
   </tr>
   <tr>
      <td>customversion</td>
      <td>字符串</td>
      <td>外部版本号；例：1.0</td>
   </tr>
   <tr>
      <td>screenwidth</td>
      <td>字符串</td>
      <td>屏幕宽度；例：240</td>
   </tr>
   <tr>
      <td>screenheight</td>
      <td>字符串</td>
      <td>屏幕高度；例：320</td>
   </tr>
   <tr>
      <td>dpi</td>
      <td>字符串</td>
      <td>手机屏幕密度，包含ldpi/mdpi/hdpi/xhdpi 四种，分别代表低分屏，中分屏，高分屏，超高分屏</td>
   </tr>
   <tr>
      <td>devicetype</td>
      <td>字符串</td>
      <td>移动设备类型，包含phone/pad  两种；例：phone</td>
   </tr>
   <tr>
      <td>clientip</td>
      <td>字符串</td>
      <td>客户端当前IP；wifi=191.168.1.1;mobile=218.94.10.103</td>
   </tr>
   <tr>
      <td>network</td>
      <td>字符串</td>
      <td>wifi、2G/3G/4G</td>
   </tr>
</table>

注：对于头信息中传中文，需要进行base64编码，且在通用头名称前加上$，如name头，ec头，其他头如果要支持传中文，也需要遵循此模式。  

响应头（表中蓝色字体部分为标准HTTP头，黑色字体为自定义通用头）  

<table>
   <tr>
      <td>名称</td>
      <td>类型</td>
      <td>值</td>
   </tr>
   <tr>
      <td><font color="blue">Server</font></td>
      <td><font color="blue">字符串</font></td>
      <td><font color="blue">服务器类型，如：Apache-Coyote/1.1</font></td>
   </tr>
   <tr>
      <td><font color="blue">Set-Cookie</font></td>
      <td><font color="blue">字符串</font></td>
      <td><font color="blue">客户端会话标识，客户端首次请求时由服务器端动态分配，在客户端后续操作中一直使用至退出客户端。格式：JSESSIONID=会话标识; Path=/process</font></td>
   </tr>
   <tr>
      <td><font color="blue">Content-Length</font></td>
      <td><font color="blue">字符串</font></td>
      <td><font color="blue">内容长度</font></td>
   </tr>
   <tr>
      <td><font color="blue">Content-Encoding</font></td>
      <td><font color="blue">字符串</font></td>
      <td><font color="blue">内容编码，此值标示响应内容是否作过编码，客户端目前只支持gzip，其值只能是gzip，如果内容未编码，则响应中没有此字段。</font></td>
   </tr>
   <tr>
      <td><font color="blue">Connection</font></td>
      <td><font color="blue">字符串</font></td>
      <td><font color="blue">客户端到服务端连接状况。值：Close或Keep-Alive，值不区分大小写。</font></td>
   </tr>
   <tr>
      <td>license</td>
      <td>字符串</td>
      <td>服务端License类型。1：正式；2：试用</td>
   </tr>
   <tr>
      <td>interfaceversion</td>
      <td>字符串</td>
      <td>客户端与服务端接口版本号；格式：x.x.x。如：4.0.0</td>
   </tr>

</table>

<h3 id="cid_0_1">示例</h3>  

```
POST /process/c HTTP/1.1
Host: 172.20.4.43:8001
User-Agent: EXMOBI-Client
Connection: keep-alive
Accept-Encoding: gzip
imsi:460004754128921
esn:354635030769800
msisdn:13900000000
$name:SmVycmll
os:android
osversion:2.2
platformid:milestone
clientid:ExMobiclient-android-000004
clientversion:3.1.0.0
screenwidth:480
screenheight:854	
	
HTTP/1.1 200 OK
Server: Apache-Coyote/1.1
license:1
interfaceversion:4.0.4
Set-Cookie: JSESSIONID=4D4612C2CA19BC5DDC33F934A19BCE0B; Path=/process
Content-Length: 206
Date: Fri, 12 Nov 2010 09:09:08 GMT
Connection: Keep-Alive
   （消息体）

```  

<h2 id="cid_1">服务访问</h2>  

<h3 id="cid_1_0">URL</h3>  

根据服务标识动态构建URL  

例：服务标识为myservice，URL取值：http://ip:port/myservice/xxxx?access_token=xxx&sso_token=xxx

<h3 id="cid_1_1">HTTP请求方式</h3>  

GET/POST  

<h3 id="cid_1_2">请求参数</h3>  

<table>
   <tr>
      <td>参数</td>
      <td>类型</td>
      <td>可选</td>
      <td>描述</td>
   </tr>
   <tr>
      <td>access_token</td>
      <td>String</td>
      <td>否</td>
      <td>访问接口凭证</td>
   </tr>
   <tr>
      <td>sso_token</td>
      <td>String</td>
      <td>是</td>
      <td>非必须字段，只有服务基于通讯录服务实现sso机制时，访问这些服务时才需要携带sso_token实现免登陆。<br/>例如：A,B服务实现sso机制，在应用调用/api/auth登陆接口后获取到sso_token后，在访问A，B服务时携带sso_token可以实现免登陆流程。</td>
   </tr>
</table>

其他请求参数根据业务确定。

<h3 id="cid_1_3">返回数据</h3>  

根据实际业务确定。

<h2 id="cid_2">/d：应用下载页面</h2>  

<h3 id="cid_2_0">说明</h3> 

平台应用下载页面地址  

<h3 id="cid_2_1">URL</h3>  

http://ip:port/d?appid=gaeaclient-ios-000005&os=ios  

<h3 id="cid_2_2">HTTP请求方式</h3>  

GET  

<h3 id="cid_2_3">请求参数</h3>  

无  

<h3 id="cid_2_4">返回数据</h3>  

应用包字节流

<h2 id="cid_3">/static：静态文件地址</h2>  

<h3 id="cid_3_0">说明</h3> 

平台静态文件访问地址  

<h3 id="cid_3_1">URL</h3>  

http://ip:port/static/xxxxx.html

<h3 id="cid_3_2">HTTP请求方式</h3>  

GET  

<h3 id="cid_3_3">请求参数</h3>  

无  

<h3 id="cid_3_4">返回数据</h3>  

静态文件体

<h2 id="cid_4">/api/auth：用户登录接口</h2>  

<h3 id="cid_4_0">说明</h3> 

该请求由应用客户端向EMP管理端发起，用于门户型客户端做用户登录。

<h3 id="cid_4_1">URL</h3>  

https://ip:port/api/auth?access_token=xxx  

说明：参数【access_token】 类型【String】 必选【是】 描述【访问接口凭证,通过URL参数携带】 

<h3 id="cid_4_2">HTTP请求方式</h3>  

GET  

<h3 id="cid_4_3">请求参数</h3>  

<table>
   <tr>
      <td>参数</td>
      <td>类型</td>
      <td>必选</td>
      <td>描述</td>
   </tr>
   <tr>
      <td>appid</td>
      <td>String</td>
      <td>是</td>
      <td>应用标识；取值参考：应用管理中的应用标识信息</td>
   </tr>
   <tr>
      <td>device</td>
      <td>String</td>
      <td>是</td>
      <td>设备标识(通常是ESN)</td>
   </tr>
   <tr>
      <td>user_account</td>
      <td>String</td>
      <td>是</td>
      <td>用户帐号</td>
   </tr>
   <tr>
      <td>password</td>
      <td>String</td>
      <td>是</td>
      <td>登录密码</td>
   </tr>
</table>  

<h3 id="cid_4_4">返回数据</h3>  

<table>
   <tr>
      <td>参数</td>
      <td>类型</td>
      <td>描述</td>
   </tr>
   <tr>
      <td>errcode</td>
      <td>int</td>
      <td>0：成功；其他参照错误访问码8300~8311</td>
   </tr>
   <tr>
      <td>errmsg</td>
      <td>String</td>
      <td>对返回码的文本描述内容</td>
   </tr>
   <tr>
      <td>sso_token</td>
      <td>String</td>
      <td>sso登录需要使用的票据</td>
   </tr>
   <tr>
      <td>expireTime</td>
      <td>String</td>
      <td>超期时间</td>
   </tr>
   <tr>
      <td>im_userid</td>
      <td>String</td>
      <td>im用户id</td>
   </tr>
   <tr>
      <td>im_sec</td>
      <td>String</td>
      <td>im描述</td>
   </tr>
   <tr>
      <td>im_username</td>
      <td>String</td>
      <td>im用户名</td>
   </tr>
</table>  

```javascript
{
    "errcode": "0",
"errmsg": "",
"sso_token": "xfafeadffaddddaaafd",
"expireTime": "2016-08-30 16:41:33",
"imUser": {
"im_userid": "846",
        "im_sec": "1d5bac9b22afed7a58db4b9dee91b975",
        "im_username": "zhangsan"
    }
}

```  

<h2 id="cid_5">/api/pwupdate：用户密码修改接口</h2>  

<h3 id="cid_5_0">说明</h3> 

该请求由应用客户端向EMP管理端发起，用于门户型客户端做用户密码修改。

<h3 id="cid_5_1">URL</h3>  

https://ip:port/api/pwupdate?access_token=xxx   

说明：参数【access_token】 类型【String】 必选【是】 描述【访问接口凭证,通过URL参数携带】   

<h3 id="cid_5_2">HTTP请求方式</h3>  

GET  

<h3 id="cid_5_3">请求参数</h3>  

<table>
   <tr>
      <td>参数</td>
      <td>类型</td>
      <td>必选</td>
      <td>描述</td>
   </tr>
   <tr>
      <td>sso_token</td>
      <td>String</td>
      <td>是</td>
      <td>登录凭证</td>
   </tr>
   <tr>
      <td>oldpw</td>
      <td>String</td>
      <td>是</td>
      <td>老密码</td>
   </tr>
   <tr>
      <td>newpw</td>
      <td>String</td>
      <td>是</td>
      <td>新密码</td>
   </tr>
   <tr>
      <td>newpw2</td>
      <td>String</td>
      <td>是</td>
      <td>再次确认新密码</td>
   </tr>
</table>  

<h3 id="cid_5_4">返回数据</h3>  

<table>
   <tr>
      <td>参数</td>
      <td>类型</td>
      <td>描述</td>
   </tr>
   <tr>
      <td>errcode</td>
      <td>int</td>
      <td>0：成功；其他参照错误访问码8300~8317</td>
   </tr>
   <tr>
      <td>errmsg</td>
      <td>String</td>
      <td>对返回码的文本描述内容</td>
   </tr>
</table>     

<h2 id="cid_6">/api/app/applatestversion：应用最新版本查询接口</h2>  

<h3 id="cid_6_0">说明</h3> 

客户端应用可以通过该接口查询到ExMobi服务端中指定应用是否有最新版本，根据响应内容，确定是否提示用户升级应用。响应中download_url字段标识了应用的下载页面。

该接口不适用于ExMobi应用和ExMobi平台型应用。

<h3 id="cid_6_1">URL</h3>  

http://ip:port/api/applatestversion?access_token=xxx&esn=xxx&imsi=xxx&appid=xxx&version=xxx    

说明：参数【access_token】 类型【String】 必选【是】 描述【访问接口凭证,通过URL参数携带】   

<h3 id="cid_6_2">HTTP请求方式</h3>  

GET  

<h3 id="cid_6_3">请求参数</h3>  

<table>
   <tr>
      <td>参数</td>
      <td>类型</td>
      <td>必选</td>
      <td>说明</td>
   </tr>
   <tr>
      <td>esn</td>
      <td>String</td>
      <td>是</td>
      <td>用户设备ESN信息<br/>无esn参数时，无法使用应用升级策略功能</td>
   </tr>
   <tr>
      <td>imsi</td>
      <td>String</td>
      <td>否</td>
      <td>用户设备IMSI信息<br/>无imsi参数时，无法使用应用升级策略功能</td>
   </tr>
   <tr>
      <td>appid</td>
      <td>String</td>
      <td>是</td>
      <td>应用标识；取值参考：应用管理中的应用标识信息</td>
   </tr>
   <tr>
      <td>version</td>
      <td>String</td>
      <td>是</td>
      <td>应用当前版本号</td>
   </tr>
</table>

<h3 id="cid_6_4">返回数据</h3>  

<table>
   <tr>
      <td>参数</td>
      <td>类型</td>
      <td>说明</td>
   </tr>
   <tr>
      <td>errcode</td>
      <td>int</td>
      <td>0成功<br/>8201：应用包系统中不存在<br/>8202：应用包版本号不能为空<br/>8203：应用包包名不能为空<br/>8204：终端未注册<br/>8205：没有更高的版本<br/>8206：没有更高的版本<br/>8207：没有更高的版本。<br/>更多请参照《ExMobi错误状态码速查.doc》</td>
   </tr>
   <tr>
      <td>errmsg</td>
      <td>String</td>
      <td>对返回码的文本描述内容</td>
   </tr>
   <tr>
      <td>app</td>
      <td>AppInfo</td>
      <td>最新版本应用对象</td>
   </tr>
</table>  

AppInfo对象定义：  

<table>
   <tr>
      <td>参数</td>
      <td>类型</td>
      <td>说明</td>
   </tr>
   <tr>
      <td>download_url</td>
      <td>int</td>
      <td>应用下载页面地址</td>
   </tr>
   <tr>
      <td>appid</td>
      <td>String</td>
      <td>应用唯一标识</td>
   </tr>
   <tr>
      <td>appname</td>
      <td>String</td>
      <td>应用名称</td>
   </tr>
   <tr>
      <td>os</td>
      <td>String</td>
      <td>操作系统   android：安卓系统  ，ios：苹果系统</td>
   </tr>
   <tr>
      <td>version</td>
      <td>String</td>
      <td>应用最高版本号</td>
   </tr>
</table>  

有最新版本，返回最新版本的应用信息： 

```javascript
{
    "errcode": "0",
    "errmsg": "成功",
"app": {
        "download_url": "http://127.0.0.1:8001/d?appid=gaeaclient-ios-000005&os=ios"
        "appid": "gaeaclient-ios-000005",
        "appname": "ExMobi客户端-iPhone",
        "version": "5.14.0.0",
        "os": "ios",
    }
}
```  

code取值8205/8206/8207，表示没有更高的版本，或者升级策略开启时判断不需要升级时响应，没有更高版本的响应可以认为是正确响应，这种情况下不提示用户升级即可。返回请求时提交版本的应用信息，download_url为""：  

```javascript
{
    "code": "8205",
    "message": "没有更高的版本",
"app": {
        "download_url": ""
        "appid": "gaeaclient-ios-000005",
        "appname": "ExMobi客户端-iPhone",
        "version": ${请求提交的version },
        "os": "ios",
    }
}
```  

应用包不存在时，返回8201，download_url为""：  

```javascript
{
    "code": "8201",
    "message": "应用包不存在",
"app": {
        "download_url": ""
        "appid": ${请求提交的appid},
        "appname": "",
        "version": ${请求提交version},
        "os": "",
    }
}
```

<h2 id="cid_7">/api/app/getapplist：查询应用列表请求</h2>  

<h3 id="cid_7_0">说明</h3>  

该请求由应用客户端向EMP管理端发起，用户在客户端中获得应用列表时候发起。  

<h3 id="cid_7_1">URL</h3>  

http://ip:port/api/app/getapplist?access_token=xxx  

说明：参数【access_token】 类型【String】 必选【是】 描述【访问接口凭证,通过URL参数携带】  

<h3 id="cid_7_2">HTTP请求方式</h3>  

POST  

<h3 id="cid_7_3">请求参数</h3>  

请求：getAppListReq  

<table>
   <tr>
      <td>参数</td>
      <td>类型</td>
      <td>必选</td>
      <td>描述</td>
   </tr>
   <tr>
      <td>version</td>
      <td>String</td>
      <td>否</td>
      <td>协议版本<br/>首次定义，默认1.0</td>
   </tr>
   <tr>
      <td>applications</td>
      <td>Application[]</td>
      <td>是</td>
      <td>已装企业应用的列表</td>
   </tr>
   <tr>
      <td>appindex</td>
      <td>int</td>
      <td>是</td>
      <td>应用当前编号，首次发起为1，加载更多时为当前应用数+1</td>
   </tr>
   <tr>
      <td>devicetype</td>
      <td>String</td>
      <td>是</td>
      <td>移动设备类型，包含phone/pad  两种；例：phone</td>
   </tr>
   <tr>
      <td>size</td>
      <td>int</td>
      <td>是</td>
      <td>每次加载的应用数 默认10</td>
   </tr>
   <tr>
      <td>Os</td>
      <td>String</td>
      <td>是</td>
      <td>操作系统，英文数字符串且全小写。详情请参看“手机操作系统定义”章节。</td>
   </tr>
   <tr>
      <td>dpi</td>
      <td>String</td>
      <td>是</td>
      <td>手机屏幕密度，包含ldpi/mdpi/hdpi/xhdpi 四种，分别代表低分屏，中分屏，高分屏，超高分屏</td>
   </tr>
</table>  

Application对象  

<table>
   <tr>
      <td>参数</td>
      <td>类型</td>
      <td>必选</td>
      <td>描述</td>
   </tr>
   <tr>
      <td>applicationid</td>
      <td>string</td>
      <td>是</td>
      <td>应用编号</td>
   </tr>
   <tr>
      <td>applicationversion</td>
      <td>String</td>
      <td>是</td>
      <td>应用版本</td>
   </tr>
   <tr>
      <td>applicationname</td>
      <td>string</td>
      <td>是</td>
      <td>应用名称</td>
   </tr>
   <tr>
      <td>applicationtype</td>
      <td>string</td>
      <td>是</td>
      <td>应用类型，1：Android应用，2：iOS应用（企业证书），3：iOS Appstore中的应用4：HTML5Web app应用，5：ExMobi应用</td>
   </tr>
</table>  

请求体示例：  

```javascript
{
    "size": 10,
    "appindex": 1,
    "applications": [
        {
            "applicationtype": "2",
            "applicationversion": "4.12.9",
            "applicationname": "安全邮件",
            "applicationid": "com.fiberhome.pushmail"
        }
    ],
    "os": "android",
    "devicetype": "phone",
    "version": "1.0",
    "dpi": "ldpi"
}
```  

<h3 id="cid_7_4">返回数据</h3>  

输出：getAppListRsp  

<table>
   <tr>
      <td>参数</td>
      <td>类型</td>
      <td>描述</td>
   </tr>
   <tr>
      <td>errcode</td>
      <td>int</td>
      <td>0：成功；-1：失败</td>
   </tr>
   <tr>
      <td>errmsg</td>
      <td>String</td>
      <td>对返回码的文本描述内容</td>
   </tr>
   <tr>
      <td>applicationInfos</td>
      <td>ApplicationInfo[]</td>
      <td>用户应用列表</td>
   </tr>
   <tr>
      <td>hasmore</td>
      <td>int</td>
      <td>是否有给更多的应用0：没有，1：有</td>
   </tr>
</table>  

ApplicationInfo对象  

<table>
   <tr>
      <td>参数</td>
      <td>类型</td>
      <td>描述</td>
   </tr>
   <tr>
      <td>appid</td>
      <td>string</td>
      <td>应用编号</td>
   </tr>
   <tr>
      <td>appname</td>
      <td>String</td>
      <td>应用名称</td>
   </tr>
   <tr>
      <td>version</td>
      <td>string</td>
      <td>version值为应用版本</td>
   </tr>
   <tr>
      <td>starnumber</td>
      <td>String</td>
      <td>评价星个数，本企业应用评价平均数，精确到小数点后一位</td>
   </tr>
   <tr>
      <td>filesize</td>
      <td>String</td>
      <td>文件大小 单位B</td>
   </tr>
   <tr>
      <td>downloadurl</td>
      <td>String</td>
      <td>资源文件下载地址，zip包</td>
   </tr>
   <tr>
      <td>artworkurl</td>
      <td>String</td>
      <td>图标地址</td>
      <td></td>
   </tr>
   <tr>
      <td>plistdownloadurl</td>
      <td>String</td>
      <td>Plist下载地址</td>
   </tr>
   <tr>
      <td>apptype</td>
      <td>string</td>
      <td>应用类型，1：Android应用，2：iOS应用（企业证书），3：iOS Appstore中的应用4：HTML5Web app应用，5：：ExMobi应用</td>
   </tr>
   <tr>
      <td>installedcount</td>
      <td>string</td>
      <td>已安装数</td>
   </tr>
   <tr>
      <td>screenshoturls</td>
      <td>String[]</td>
      <td>详细图片地址</td>
   </tr>
   <tr>
      <td>appentryreg</td>
      <td>string</td>
      <td>Ios程序注册入口</td>
   </tr>
</table>  

响应体示例：  

```javascript
{
    "applicationinfos": [
        {
            "appid": "com.gionee.aora.weather",
            "appname": "易天气",
            "apptype": "1",
            "artworkurl": "http://127.0.0.1:8001/iosimg.jsp?path=l1t3dNjR4ak2v1vdY61rUHBVvktu0SzC2MWVPD9RIboAXF-1I2zSwl0ZmPyunEN8baoQH32SQyJHVJ_cQGEWcKcHSgRKL-45_BSALaPYEag1llHo92ZmlvnoZNUr9jfnhz4bxnUK-y8",
            "briefdescription": "12121",
            "comments": "0",
            "downloadurl": "http://127.0.0.1:8001/commonDownload.action?type=3&filetype=zip&appId=com.gionee.aora.weather",
            "filesize": "4061339",
            "installedcount": "0",
            "releasedate": "2016-12-19",
            "screenshoturls": [],
            "starnumber": "0",
            "version": "2.1.9.0"
        }
    ],
    "errcode": "0",
    "errmsg": "获取应用列表成功",
    "hasmore": 0,
    "totalsize": 1
}
```  

<h2 id="cid_8">/api/app/getappdetails：查询应用详情请求</h2>  

<h3 id="cid_8_0">说明</h3>  

该请求由客户端向EMP管理端发起，用户在客户端中获得应用列表时候发起。 

<h3 id="cid_8_1">URL</h3>  

http://ip:port/api/app/getappdetails?access_token=xxx  

说明：参数【access_token】 类型【String】 必选【是】 描述【访问接口凭证,通过URL参数携带】  

<h3 id="cid_8_2">HTTP请求方式</h3>  

POST  

<h3 id="cid_8_3">请求参数</h3>  

请求：getAppDetailsReq  

<table>
   <tr>
      <td>参数</td>
      <td>类型</td>
      <td>必选</td>
      <td>描述</td>
   </tr>
   <tr>
      <td>version</td>
      <td>String</td>
      <td>否</td>
      <td>协议版本；首次定义，默认1.0</td>
   </tr>
   <tr>
      <td>appid</td>
      <td>String</td>
      <td></td>
      <td>应用id</td>
   </tr>
   <tr>
      <td>apptype</td>
      <td>String</td>
      <td>是</td>
      <td>应用类型，1：Android应用，2：iOS应用（企业证书），3：iOS Appstore中的应用4：HTML5Web app应用，5：：ExMobi应用</td>
   </tr>
   <tr>
      <td>devicetype</td>
      <td>String</td>
      <td>是</td>
      <td>移动设备类型，包含phone/pad  两种；例：phone</td>
   </tr>
   <tr>
      <td>os</td>
      <td>String</td>
      <td>是</td>
      <td>操作系统，英文数字符串且全小写。详情请参看“手机操作系统定义”章节。</td>
   </tr>
   <tr>
      <td>dpi</td>
      <td>String</td>
      <td>是</td>
      <td>手机屏幕密度，包含ldpi/mdpi/hdpi/xhdpi 四种，分别代表低分屏，中分屏，高分屏，超高分屏</td>
   </tr>
</table>  

请求体示例：

```javascript
{
    "appid": "com.fiberhome.gaea.client",
    "os": "android",
    "version": "1.0",
    "devicetype": "phone",
    "apptype": "1"
}
```

<h3 id="cid_8_4">返回数据</h3>  

输出：getAppDetailsResp  

<table>
   <tr>
      <td>参数</td>
      <td>类型</td>
      <td>描述</td>
   </tr>
   <tr>
      <td>errcode</td>
      <td>int</td>
      <td>0：成功；-1：失败</td>
   </tr>
   <tr>
      <td>errmsg</td>
      <td>String</td>
      <td>对返回码的文本描述内容</td>
   </tr>
   <tr>
      <td>version</td>
      <td>String</td>
      <td>版本号</td>
   </tr>
   <tr>
      <td>briefdescription</td>
      <td>String</td>
      <td>介绍</td>
   </tr>
   <tr>
      <td>starnumber</td>
      <td>String</td>
      <td>评价星个数，本企业应用评价平均数，精确到小数点后一位</td>
   </tr>
   <tr>
      <td>comments</td>
      <td>String</td>
      <td>评论数</td>
   </tr>
   <tr>
      <td>commentinfos</td>
      <td>AppCommentInfo[]</td>
      <td>评论集合，为最新的10条评论</td>
   </tr>
   <tr>
      <td>screenshoturls</td>
      <td>String[]</td>
      <td>详细图片地址</td>
   </tr>
   <tr>
      <td>releasedate</td>
      <td>String</td>
      <td>发布时间</td>
   </tr>
   <tr>
      <td>filesize</td>
      <td>String</td>
      <td>文件大小 单位K</td>
   </tr>
   <tr>
      <td>updatelog</td>
      <td>String</td>
      <td>最新版本变更说明</td>
   </tr>
   <tr>
      <td>installedcount</td>
      <td>string</td>
      <td>已安装数</td>
   </tr>
</table>  

AppCommentInfo对象  

<table>
   <tr>
      <td>参数</td>
      <td>类型</td>
      <td>描述</td>
   </tr>
   <tr>
      <td>loginid</td>
      <td>String</td>
      <td>评论用户ID</td>
   </tr>
   <tr>
      <td>starnumber</td>
      <td>String</td>
      <td>评价星个数 </td>
   </tr>
   <tr>
      <td>commentinfo</td>
      <td>String</td>
      <td>评论内容</td>
   </tr>
   <tr>
      <td>commenttime</td>
      <td>String</td>
      <td>评论时间</td>
   </tr>
</table>  

响应体示例：  

```javascript
{
    "appid": "com.gionee.aora.weather",
    "appname": "易天气",
    "apptype": "1",
    "artworkurl": "http://127.0.0.1:8001/iosimg.jsp?path=l1t3dNjR4ak2v1vdY61rUHBVvktu0SzC2MWVPD9RIboAXF-1I2zSwl0ZmPyunEN8baoQH32SQyJHVJ_cQGEWcKcHSgRKL-45_BSALaPYEag1llHo92ZmlvnoZNUr9jfnhz4bxnUK-y8",
    "briefdescription": "12121",
    "commentinfos": [],
    "comments": "0",
    "downloadurl": "http://127.0.0.1:8001/commonDownload.action?type=3&filetype=zip&appId=com.gionee.aora.weather",
    "errcode": "0",
    "errmsg": "获取详情列表成功",
    "filesize": "4061339",
    "installedcount": "0",
    "releasedate": "2016-12-19",
    "screenshoturls": [
        "http://127.0.0.1:8001/iosimg.jsp?path=l1t3dNjR4ak2v1vdY61rUHBVvktu0SzC2MWVPD9RIboAXF-1I2zSwl0ZmPyunEN8baoQH32SQyJHVJ_cQGEWcKcHSgRKL-45_BSALaPYEag1llHo92ZmlnBxhM7qkaWP78nlhXie_52IYf4uId8S9fPV4UyQWcUy5-Xveim9-r4"
    ],
    "starnumber": "0",
    "version": "2.1.9.0"
}
```  

<h2 id="cid_9">/api/app/getappcategorylist：查询应用分类请求</h2>  

<h3 id="cid_9_0">说明</h3>  

该请求由应用客户端向EMP管理端发起，用户在客户端中刷新应用分组列表时候发起。   

<h3 id="cid_9_1">URL</h3>  

http://ip:port/api/app/getappcategorylist?access_token=xxx   

说明：参数【access_token】 类型【String】 必选【是】 描述【访问接口凭证,通过URL参数携带】  

<h3 id="cid_9_2">HTTP请求方式</h3>  

POST  

<h3 id="cid_9_3">请求参数</h3>  

请求：getAppCategoryListReq  

<table>
   <tr>
      <td>参数</td>
      <td>类型</td>
      <td>必选</td>
      <td>描述</td>
   </tr>
   <tr>
      <td>version</td>
      <td>String</td>
      <td>否</td>
      <td>协议版本<br/>首次定义，默认1.0</td>
   </tr>
</table>  

请求体示例：  

```javascript
{"version":"1.0"}
```

<h3 id="cid_9_4">返回数据</h3>  

输出：getAppCategoryListRsp  

<table>
   <tr>
      <td>参数</td>
      <td>类型</td>
      <td>描述</td>
   </tr>
   <tr>
      <td>errcode</td>
      <td>int</td>
      <td>0：成功；-1：失败</td>
   </tr>
   <tr>
      <td>errmsg</td>
      <td>String</td>
      <td>对返回码的文本描述内容</td>
   </tr>
   <tr>
      <td>applicationcategory</td>
      <td>ApplicationCategory[]</td>
      <td>用户应用类别列表</td>
   </tr>
</table>  

ApplicationCategory对象  

<table>
   <tr>
      <td>参数</td>
      <td>类型</td>
      <td>描述</td>
   </tr>
   <tr>
      <td>appcategory</td>
      <td>String</td>
      <td>应用类别名称</td>
   </tr>
   <tr>
      <td>artworkrul </td>
      <td>String</td>
      <td>应用类别图标地址</td>
   </tr>
</table>  

响应体示例：  

```javascript
{
    "applicationcategory": [
        {
            "appcategory": "推荐应用",
            "artworkrul": "http://127.0.0.1:8001/emp_jsp/clientdownload/exmobi.png"
        },
        {
            "appcategory": "项目类别",
            "artworkrul": "http://127.0.0.1:8001/emp_jsp/clientdownload/exmobi.png"
        }
    ],
    "errcode": "0",
    "errmsg": "获取类别列表成功"
}
```  

<h2 id="cid_10">/api/app/getapplistbycategory：根据分类查询应用列表请求</h2>  

<h3 id="cid_10_0">说明</h3>  

该请求由应用客户端向EMP管理端发起，用户在客户端中获得应用列表时候发起。  

<h3 id="cid_10_1">URL</h3>  

http://ip:port/api/app/getapplistbycategory?access_token=xxx    

说明：参数【access_token】 类型【String】 必选【是】 描述【访问接口凭证,通过URL参数携带】  

<h3 id="cid_10_2">HTTP请求方式</h3>  

POST  

<h3 id="cid_10_3">请求参数</h3>  

请求：getAppListReq  

<table>
   <tr>
      <td>参数</td>
      <td>类型</td>
      <td>必选</td>
      <td>描述</td>
   </tr>
   <tr>
      <td>version</td>
      <td>String</td>
      <td>否</td>
      <td>协议版本；首次定义，默认1.0</td>
   </tr>
   <tr>
      <td>applications</td>
      <td>Application[]</td>
      <td>是</td>
      <td>已装应用的列表</td>
   </tr>
   <tr>
      <td>appcategory</td>
      <td>String</td>
      <td>是</td>
      <td>应用类别名称</td>
   </tr>
   <tr>
      <td>appindex</td>
      <td>Int</td>
      <td>是</td>
      <td>页号，首次发起为1，加载更多时为当前页号+1</td>
   </tr>
   <tr>
      <td>size</td>
      <td>Int</td>
      <td>是</td>
      <td>每次加载的应用数 10</td>
   </tr>
<tr>
      <td>devicetype</td>
      <td>String</td>
      <td>是</td>
      <td>移动设备类型，包含phone/pad  两种</td>
   </tr>
   <tr>
      <td>Os</td>
      <td>String</td>
      <td>是</td>
      <td>操作系统，英文数字符串且全小写。详情请参看“手机操作系统定义”章节。</td>
   </tr>
   <tr>
      <td>dpi</td>
      <td>String</td>
      <td>是</td>
      <td>手机屏幕密度，包含ldpi/mdpi/hdpi/xhdpi 四种，分别代表低分屏，中分屏，高分屏，超高分屏</td>
   </tr>
</table>  

Application对象  

<table>
   <tr>
      <td>参数</td>
      <td>类型</td>
      <td>描述</td>
   </tr>
   <tr>
      <td>applicationid</td>
      <td>String</td>
      <td>应用编号</td>
   </tr>
   <tr>
      <td>applicationversion</td>
      <td>String</td>
      <td>应用版本</td>
   </tr>
   <tr>
      <td>applicationname</td>
      <td>String</td>
      <td>应用名称</td>
   </tr>
   <tr>
      <td>applicationtype</td>
      <td>String</td>
      <td>应用类型，1：Android应用，2：iOS应用（企业证书），3：iOS Appstore中的应用4：HTML5Web app应用，5：：ExMobi应用</td>
   </tr>
</table>  

请求体示例：  

```javascript
{
    "size": 15,
    "appindex": 1,
    "appcategory": "推荐应用",
    "applications": [
        {
            "applicationtype": "2",
            "applicationversion": "4.12.9",
            "applicationname": "安全邮件",
            "applicationid": "com.fiberhome.pushmail"
        }
    ],
    "version": "1.0",
    "os": "android",
    "devicetype": "phone",
    "dpi": "ldpi"
}
```

<h3 id="cid_10_4">返回数据</h3>  

输出：getAppListRsp  

<table>
   <tr>
      <td></td>
      <td>参数</td>
      <td>类型</td>
      <td>描述</td>
   </tr>
   <tr>
      <td>errcode</td>
      <td>int</td>
      <td>0：成功；-1：失败</td>
   </tr>
   <tr>
      <td>errmsg</td>
      <td>String</td>
      <td>对返回码的文本描述内容</td>
   </tr>
   <tr>
      <td>applicationinfos</td>
      <td>ApplicationInfo[]</td>
      <td>用户应用列表</td>
   </tr>
   <tr>
      <td>hasmore</td>
      <td>Int</td>
      <td>是否有给更多的引用0：没有，1：有</td>
   </tr>
</table>  

ApplicationInfo对象  

<table>
   <tr>
      <td>参数</td>
      <td>类型</td>
      <td>描述</td>
   </tr>
   <tr>
      <td>appid</td>
      <td>String</td>
      <td>应用编号</td>
   </tr>
   <tr>
      <td>appname</td>
      <td>String</td>
      <td>应用名称</td>
   </tr>
   <tr>
      <td>version</td>
      <td>String</td>
      <td>version值为应用版本</td>
   </tr>
   <tr>
      <td>starnumber</td>
      <td>String</td>
      <td>评价星个数，本企业应用评价平均数，精确到小数点后一位</td>
   </tr>
   <tr>
      <td>filesize</td>
      <td>String</td>
      <td>文件大小 单位K</td>
   </tr>
   <tr>
      <td>downloadurl</td>
      <td>String</td>
      <td>资源文件下载地址，zip包</td>
   </tr>
   <tr>
      <td>artworkurl</td>
      <td> String</td>
      <td>图标地址</td>
   </tr>
   <tr>
      <td>plistdownloadurl</td>
      <td>String</td>
      <td>Plist下载地址</td>
   </tr>
   <tr>
      <td>apptype</td>
      <td>String</td>
      <td>应用类型，1：Android应用，2：iOS应用（企业证书），3：iOS Appstore中的应用4：HTML5Web app应用，5：：ExMobi应用</td>
   </tr>
   <tr>
      <td>installedcount</td>
      <td>string</td>
      <td>已安装数</td>
   </tr>
</table>  

响应体示例：  

```javascript
{
    "applicationinfos": [
        {
            "appid": "com.gionee.aora.weather",
            "appname": "易天气",
            "apptype": "1",
            "artworkurl": "http://127.0.0.1:8001/iosimg.jsp?path=l1t3dNjR4ak2v1vdY61rUHBVvktu0SzC2MWVPD9RIboAXF-1I2zSwl0ZmPyunEN8baoQH32SQyJHVJ_cQGEWcKcHSgRKL-45_BSALaPYEag1llHo92ZmlvnoZNUr9jfnhz4bxnUK-y8",
            "comments": "0",
            "downloadurl": "http://127.0.0.1:8001/commonDownload.action?type=3&filetype=zip&appId=com.gionee.aora.weather",
            "filesize": "4061339",
            "installedcount": "0",
            "screenshoturls": [
                "http://127.0.0.1:8001/iosimg.jsp?path=l1t3dNjR4ak2v1vdY61rUHBVvktu0SzC2MWVPD9RIboAXF-1I2zSwl0ZmPyunEN8baoQH32SQyJHVJ_cQGEWcKcHSgRKL-45_BSALaPYEag1llHo92ZmlnBxhM7qkaWP78nlhXie_52IYf4uId8S9fPV4UyQWcUy5-Xveim9-r4"
            ],
            "starnumber": "0",
            "version": "2.1.9.0"
        }
    ],
    "errcode": "0",
    "errmsg": "获取应用列表成功",
    "hasmore": 0,
    "totalsize": 1
}

```

<h2 id="cid_11">/api/app/getapplistforkeyword：根据关键字查询应用请求</h2>  

<h3 id="cid_11_0">说明</h3>  

该请求由应用客户端向EMP管理端发起，用户在客户端中根据关键字查询是发起   

<h3 id="cid_11_1">URL</h3>  

http://ip:port/api/app/getapplistforkeyword?access_token=xxx 

说明：参数【access_token】 类型【String】 必选【是】 描述【访问接口凭证,通过URL参数携带】  

<h3 id="cid_11_2">HTTP请求方式</h3>  

POST  

<h3 id="cid_11_3">请求参数</h3>  

请求：getAppListForKeywordReq  

<table>
   <tr>
      <td>参数</td>
      <td>类型</td>
      <td>必选</td>
      <td>描述</td>
   </tr>
   <tr>
      <td>version</td>
      <td>String</td>
      <td>否</td>
      <td>协议版本；首次定义，默认1.0</td>
   </tr>
   <tr>
      <td>keyword</td>
      <td>String</td>
      <td>是</td>
      <td>关键字</td>
   </tr>
   <tr>
      <td>applications</td>
      <td>Application[]</td>
      <td>是</td>
      <td>已装应用的列表</td>
   </tr>
   <tr>
      <td>devicetype</td>
      <td>String</td>
      <td>是</td>
      <td>移动设备类型，包含phone/pad  两种</td>
   </tr>
   <tr>
      <td>Os</td>
      <td>String</td>
      <td>是</td>
      <td>操作系统，英文数字符串且全小写。详情请参看“手机操作系统定义”章节。</td>
   </tr>
   <tr>
      <td>dpi</td>
      <td>String</td>
      <td>是</td>
      <td>手机屏幕密度，包含ldpi/mdpi/hdpi/xhdpi 四种，分别代表低分屏，中分屏，高分屏，超高分屏</td>
   </tr>
</table>  

Application对象  

<table>
   <tr>
      <td>参数</td>
      <td>类型</td>
      <td>必选</td>
      <td>描述</td>
   </tr>
   <tr>
      <td>applicationid</td>
      <td>String</td>
      <td>是</td>
      <td>应用编号</td>
   </tr>
   <tr>
      <td>applicationversion</td>
      <td>String</td>
      <td>是</td>
      <td>应用版本</td>
   </tr>
   <tr>
      <td>applicationname</td>
      <td>String</td>
      <td>是</td>
      <td>应用名称</td>
   </tr>
   <tr>
      <td>applicationtype</td>
      <td>String</td>
      <td>是</td>
      <td>应用类型，1：Android应用，2：iOS应用（企业证书），3：iOS Appstore中的应用4：HTML5Web app应用，5：ExMobi应用</td>
   </tr>
</table>  

请求体示例：  

```javascript
{
    "keyword": "db",
    "os": "ios",
    "devicetype": "pad",
    "dpi": "ldpi",
    "applications": [],
    "version": "1.0"
}
```

<h3 id="cid_11_4">返回数据</h3>  

getAppListForKeywordRsp  

<table>
   <tr>
      <td>参数</td>
      <td>类型</td>
      <td>描述</td>
   </tr>
   <tr>
      <td>errcode</td>
      <td>int</td>
      <td>0：成功；-1：失败</td>
   </tr>
   <tr>
      <td>errmsg</td>
      <td>String</td>
      <td>对返回码的文本描述内容</td>
   </tr>
   <tr>
      <td>applicationinfos</td>
      <td>ApplicationInfo[]</td>
      <td>用户应用列表</td>
   </tr>
   <tr>
      <td>hasmore</td>
      <td>Int</td>
      <td>是否有给更多的引用0：没有，1：有</td>
   </tr>
</table>  

ApplicationInfo对象  

<table>
   <tr>
      <td>参数</td>
      <td>类型</td>
      <td>描述</td>
   </tr>
   <tr>
      <td>appid</td>
      <td>String</td>
      <td>应用编号</td>
   </tr>
   <tr>
      <td>appname</td>
      <td>String</td>
      <td>应用名称</td>
   </tr>
   <tr>
      <td>version</td>
      <td>String</td>
      <td>version值为应用版本</td>
   </tr>
   <tr>
      <td>starnumber</td>
      <td>String</td>
      <td>评价星个数，本企业应用评价平均数，精确到小数点后一位</td>
   </tr>
   <tr>
      <td>filesize</td>
      <td>String</td>
      <td>文件大小 单位K</td>
   </tr>
   <tr>
      <td>downloadurl</td>
      <td>String</td>
      <td>资源文件下载地址，zip包</td>
   </tr>
   <tr>
      <td>artworkurl</td>
      <td> String</td>
      <td>图标地址</td>
   </tr>
   <tr>
      <td>plistdownloadurl</td>
      <td>String</td>
      <td>Plist下载地址</td>
   </tr>
   <tr>
      <td>apptype</td>
      <td>String</td>
      <td>应用类型，1：ExMobi应用，2：Android应用，3：iOS应用（企业证书），4：HTML5Web app应用，5：iOS Appstore中的应用</td>
   </tr>
</table>  

响应体示例：  

```javacript
{
    "applicationinfos": [
        {
            "appid": "db",
            "appname": "db",
            "apptype": "5",
            "artworkurl": "http://127.0.0.1:8001/emp_jsp/clientdownload/exmobi.png",
            "briefdescription": "212121212",
            "comments": "0",
            "downloadurl": "http://127.0.0.1:8001/commonDownload.action?type=9&filetype=zip&appId=db&devicetype=pad&dpi=ldpi",
            "filesize": "900",
            "installedcount": "0",
            "releasedate": "2016-12-05",
            "screenshoturls": [],
            "starnumber": "0",
            "version": "1.0.0"
        }
    ],
    "errcode": "0",
    "errmsg": "获取应用列表成功",
    "hasmore": 0,
    "totalsize": 1
}
```  

<h2 id="cid_12">/api/app/getappupdatelist：查询应用升级列表请求</h2>  

<h3 id="cid_12_0">说明</h3>  

该请求由应用客户端向EMP管理端发起，用户获得应用升级列表，客户端传入已装应用列表和版本，服务端给出这些应用中需要升级的应用列表，在应用安装完成和卸载完成后，在后台调用下该接口，及时上报客户端的最新应用信息。    

<h3 id="cid_12_1">URL</h3>  

http://ip:port/api/app/getappupdatelist?access_token=xxx   

说明：参数【access_token】 类型【String】 必选【是】 描述【访问接口凭证,通过URL参数携带】  

<h3 id="cid_12_2">HTTP请求方式</h3>  

POST  

<h3 id="cid_12_3">请求参数</h3>  

请求：getAppUpdateListReq  

<table>
   <tr>
      <td>参数</td>
      <td>类型</td>
      <td>必选</td>
      <td>描述</td>
   </tr>
   <tr>
      <td>version</td>
      <td>String</td>
      <td>否</td>
      <td>协议版本；首次定义，默认1.0</td>
   </tr>
   <tr>
      <td>applications</td>
      <td>Application[]</td>
      <td>是</td>
      <td>已装应用的列表</td>
   </tr>
   <tr>
      <td>devicetype</td>
      <td>String</td>
      <td>是</td>
      <td>移动设备类型，包含phone/pad  两种</td>
   </tr>
   <tr>
      <td>Os</td>
      <td>String</td>
      <td>是</td>
      <td>操作系统，英文数字符串且全小写。详情请参看“手机操作系统定义”章节。</td>
   </tr>
   <tr>
      <td>dpi</td>
      <td>String</td>
      <td>是</td>
      <td>手机屏幕密度，包含ldpi/mdpi/hdpi/xhdpi 四种，分别代表低分屏，中分屏，高分屏，超高分屏</td>
   </tr>
</table>  

Application对象  

<table>
   <tr>
      <td>参数</td>
      <td>类型</td>
      <td>必选</td>
      <td>描述</td>
   </tr>
   <tr>
      <td>applicationid</td>
      <td>String</td>
      <td>是</td>
      <td>应用编号</td>
   </tr>
   <tr>
      <td>applicationversion</td>
      <td>String</td>
      <td>是</td>
      <td>应用版本</td>
   </tr>
   <tr>
      <td>applicationname</td>
      <td>String</td>
      <td>是</td>
      <td>应用名称</td>
   </tr>
   <tr>
      <td>applicationtype</td>
      <td>String</td>
      <td>是</td>
      <td>应用类型，1：Android应用，2：iOS应用（企业证书），3：iOS Appstore中的应用4：HTML5Web app应用，5：ExMobi应用</td>
   </tr>
</table>  

请求体示例：  

```javascript
{
    "applications": [
     {
     Applicationid：baiduMap,
     Applicationversion:2.3.0,
     Applicationname:百度地图,
     Applicationtype:1
     },
     {
     Applicationid：wangyinews,
     Applicationversion:4.3.0,
     Applicationname:网易新闻,
     Applicationtype:2
     },......
     ],
    "version": "1.0"
}
```

<h3 id="cid_12_4">返回数据</h3>  

输出：getAppUpdateListRsp  

<table>
   <tr>
      <td>参数</td>
      <td>类型</td>
      <td>描述</td>
   </tr>
   <tr>
      <td>errcode</td>
      <td>int</td>
      <td>0：成功；-1：失败</td>
   </tr>
   <tr>
      <td>errmsg</td>
      <td>String</td>
      <td>对返回码的文本描述内容</td>
   </tr>
   <tr>
      <td>upgradeapps</td>
      <td>UpgradeApplication[]</td>
      <td>待升级应用列表</td>
   </tr>
   <tr>
      <td>installapps</td>
      <td>InstallApplication[]</td>
      <td>待安装应用列表（系统已经安装，并且存在URLScheme但工作台未展示）</td>
   </tr>
   <tr>
      <td>uninstallapps</td>
      <td>UninstallApplication[]</td>
      <td>待卸载的应用列表</td>
   </tr>
   <tr>
      <td>mustinstallapps</td>
      <td>InstallApplication []</td>
      <td>必装应用列表</td>
   </tr>
   <tr>
      <td>params</td>
      <td>UserParam[]</td>
      <td>应用参数列表</td>
   </tr>
</table>  

UpgradeApplication对象  

<table>
   <tr>
      <td>参数</td>
      <td>类型</td>
      <td>描述</td>
   </tr>
   <tr>
      <td>appid</td>
      <td>String</td>
      <td>应用编号</td>
   </tr>
   <tr>
      <td>appname</td>
      <td>String</td>
      <td>应用名称</td>
   </tr>
   <tr>
      <td>latestversion</td>
      <td>String</td>
      <td>最新应用版本 </td>
   </tr>
   <tr>
      <td>downloadurl</td>
      <td>String</td>
      <td>如果存在更高版本，则提供该信息，下载地址</td>
   </tr>
   <tr>
      <td>plistdownloadurl</td>
      <td>String</td>
      <td>Plist下载地址</td>
   </tr>
   <tr>
      <td>updatelog</td>
      <td> String</td>
      <td>更新说明</td>
   </tr>
   <tr>
      <td>apptype</td>
      <td>String</td>
      <td>如果存在更高版本，则提供该信息，应用类型，1：Android应用，2：iOS应用（企业证书），3：iOS Appstore中的应用4：HTML5Web app应用，5：ExMobi应用</td>
   </tr>
   <tr>
      <td>filesize</td>
      <td>String</td>
      <td>文件大小 单位K</td>
   </tr>
</table>  

InstallApplication对象  

<table>
   <tr>
      <td>参数</td>
      <td>类型</td>
      <td>描述</td>
   </tr>
   <tr>
      <td>appid</td>
      <td>String</td>
      <td>应用编号</td>
   </tr>
   <tr>
      <td>appname</td>
      <td>String</td>
      <td>应用名称</td>
   </tr>
   <tr>
      <td>appversion</td>
      <td>String</td>
      <td>最新应用版本 </td>
   </tr>
   <tr>
      <td>downloadurl</td>
      <td>String</td>
      <td>下载地址</td>
   </tr>
   <tr>
      <td>plistdownloadurl</td>
      <td>String</td>
      <td>Plist下载地址</td>
   </tr>
   <tr>
      <td>apptype</td>
      <td>String</td>
      <td>应用类型，1：Android应用，2：iOS应用（企业证书），3：iOS Appstore中的应用4：HTML5Web app应用，5：ExMobi应用</td>
   </tr>
</table>  

UninstallApplication对象  

<table>
   <tr>
      <td>参数</td>
      <td>类型</td>
      <td>描述</td>
   </tr>
   <tr>
      <td>appid</td>
      <td>String</td>
      <td>应用编号</td>
   </tr>
   <tr>
      <td>appname</td>
      <td>String</td>
      <td>应用名称</td>
   </tr>
   <tr>
      <td>apptype</td>
      <td>String</td>
      <td>应用类型，1：Android应用，2：iOS应用（企业证书），3：iOS Appstore中的应用4：HTML5Web app应用，5：ExMobi应用</td>
   </tr>
</table>  

UserParam对象  

<table>
   <tr>
      <td>参数</td>
      <td>类型</td>
      <td>描述</td>
   </tr>
   <tr>
      <td>appid</td>
      <td>String</td>
      <td>应用编号</td>
   </tr>
   <tr>
      <td>paramkey</td>
      <td> String</td>
      <td>参数名称</td>
   </tr>
   <tr>
      <td>paramvalue</td>
      <td>String</td>
      <td>参数值</td>
   </tr>
</table>  

响应体示例：  

```javascript
{
    "errcode": "0",
    "errmsg": "获取升级列表成功",
    "installapps": [],
    "mustinstallapps": [],
    "params": [
        {
            "appid": "cn.com.fiberhome.nj.mapclient.GAEA",
            "paramkey": "a",
            "paramvalue": "admin111"
        },
        {
            "appid": "cn.com.fiberhome.nj.mapclient.GAEA",
            "paramkey": "b",
            "paramvalue": "admin111"
        }
    ],
    "uninstallapps": [],
    "upgradeapps": [
        {
            "appid": "cn.com.fiberhome.nj.mapclient.GAEA",
            "appname": "ExMobi",
            "apptype": "2",
            "artworkurl": "http://127.0.0.1:8001/iosimg.jsp?path=l1t3dNjR4ak2v1vdY61rUHBVvktu0SzC2MWVPD9RIboAXF-1I2zSwl0ZmPyunEN8Qk79FkHG1UZzN3kH7dcpq3_Q47DnoHupliOZeSCjtAi3ZzDEs1T7JeMqBlcuvC7LxYlOLd3mhN2HPhvGdQr7Lw",
            "filesize": "42084479",
            "latestversion": "5.15.1.0",
            "plistdownloadurl": "https://127.0.0.1:8443/commonDownload.action/cn.com.fiberhome.nj.mapclient.GAEA.plist",
            "updateflag": "0",
            "updatelog": ""
        }
    ]
}
```

<h2 id="cid_13">/api/app/checkappinfo：应用信息确认请求</h2>  

<h3 id="cid_13_0">说明</h3>  

该请求由应用客户端向EMP管理端发起,在进入应用前进行应用信息确认，主要功能为检测该用户是否有权限登录该应用，该用户可是使用该应用的模块列表，查看该应用是否有更高版本。   

<h3 id="cid_13_1">URL</h3>  

http://ip:port/api/app/checkappinfo?access_token=xxx   

说明：参数【access_token】 类型【String】 必选【是】 描述【访问接口凭证,通过URL参数携带】  

<h3 id="cid_13_2">HTTP请求方式</h3>  

POST  

<h3 id="cid_13_3">请求参数</h3>  

请求：CheckAppInfoReq  

<table>
   <tr>
      <td>参数</td>
      <td>类型</td>
      <td>必选</td>
      <td>描述</td>
   </tr>
   <tr>
      <td>version</td>
      <td>String</td>
      <td>否</td>
      <td>协议版本；首次定义，默认1.0</td>
   </tr>
   <tr>
      <td>appid</td>
      <td>String</td>
      <td>是</td>
      <td>应用ID</td>
   </tr>
   <tr>
      <td>appVersion</td>
      <td>String</td>
      <td>是</td>
      <td>应用版本</td>
   </tr>
   <tr>
      <td>apptype</td>
      <td>String</td>
      <td>是</td>
      <td>应用类型  应用类型，1：ExMobi应用，2：Android应用，3：iOS应用（企业证书），4：HTML5Web app应用，5：iOS Appstore中的应用</td>
   </tr>
   <tr>
      <td>scheme</td>
      <td>String</td>
      <td>否</td>
      <td>客户端希望的启动传参内容，携带该参数则忽略服务器配的启动传参内容，使用该内容进行参数替换，然后在响应中的scheme返回。</td>
   </tr>
</table>  

<h3 id="cid_13_4">返回数据</h3>  

输出：CheckAppInfoRsp  

<table>
   <tr>
      <td>参数</td>
      <td>类型</td>
      <td>描述</td>
   </tr>
   <tr>
      <td>errcode</td>
      <td>int</td>
      <td>返回码 0：允许接入 1：禁止使用该应用 -1：系统正忙，请稍后再试！</td>
   </tr>
   <tr>
      <td>errmsg</td>
      <td>String</td>
      <td>对返回码的文本描述内容</td>
   </tr>
   <tr>
      <td>latestversion</td>
      <td>String</td>
      <td>最新应用版本，如果不存在更高版本则为空</td>
   </tr>
   <tr>
      <td>downloadurl</td>
      <td>String</td>
      <td>如果存在更高版本，则提供该信息，下载地址</td>
   </tr>
   <tr>
      <td>plistdownloadurl</td>
      <td>String</td>
      <td>plist下载地址</td>
   </tr>
   <tr>
      <td>updatescription</td>
      <td>String</td>
      <td>更新描述</td>
   </tr>
   <tr>
      <td>filesize</td>
      <td>String</td>
      <td>文件大小 单位K</td>
   </tr>
   <tr>
      <td>scheme</td>
      <td>String</td>
      <td>打开应用时传参,需要替换变量${username}、${password}</td>
   </tr>
</table>  

<h2 id="cid_14">/api/app/getappevaluation：获取应用使用评价请求</h2>  

<h3 id="cid_14_0">说明</h3>  

该请求由应用客户端向EMP管理端发起，用于终端用户获取应用更多使用评价，用于展示第11条以后的评论，前10条在应用详情接口已返回。 

<h3 id="cid_14_1">URL</h3>  

http://ip:port/api/app/getappevaluation?access_token=xxx  

说明：参数【access_token】 类型【String】 必选【是】 描述【访问接口凭证,通过URL参数携带】  

<h3 id="cid_14_2">HTTP请求方式</h3>  

POST  

<h3 id="cid_14_3">请求参数</h3>  

请求：getAppEvaluationReq  

<table>
   <tr>
      <td>参数</td>
      <td>类型</td>
      <td>必选</td>
      <td>描述</td>
   </tr>
   <tr>
      <td>version</td>
      <td>String</td>
      <td>否</td>
      <td>协议版本；首次定义，默认1.0</td>
   </tr>
   <tr>
      <td>appid</td>
      <td>String</td>
      <td>是</td>
      <td>应用编号</td>
   </tr>
   <tr>
      <td>appversion</td>
      <td>String</td>
      <td>是</td>
      <td>应用版本</td>
   </tr>
   <tr>
      <td>apptype</td>
      <td>String</td>
      <td>是</td>
      <td>应用类型，1：Android应用，2：iOS应用（企业证书），3：iOS Appstore中的应用4：HTML5Web app应用，5：：ExMobi应用</td>
   </tr>
   <tr>
      <td>appindex</td>
      <td>int</td>
      <td>是</td>
      <td>评论编号，从1开始，用于分页</td>
   </tr>
   <tr>
      <td>size</td>
      <td>int</td>
      <td>是</td>
      <td>每次加载的数 默认10</td>
   </tr>
</table>

<h3 id="cid_14_4">返回数据</h3>  

输出：getAppEvaluationRsp  

<table>
   <tr>
      <td>参数</td>
      <td>类型</td>
      <td>描述</td>
   </tr>
   <tr>
      <td>errcode</td>
      <td>int</td>
      <td>0：成功；-1：失败</td>
   </tr>
   <tr>
      <td>errmsg</td>
      <td>String</td>
      <td>对返回码的文本描述内容</td>
   </tr>
   <tr>
      <td>starnumber</td>
      <td>String</td>
      <td>评价星个数，本企业应用评价平均数，精确到小数点后一位</td>
   </tr>
   <tr>
      <td>commentinfos</td>
      <td>AppCommentInfo[]</td>
      <td>评论集合</td>
   </tr>
   <tr>
      <td>hasmore</td>
      <td>int</td>
      <td>是否有给更多 0：没有，1：有</td>
   </tr>
</table>  

AppCommentInfo对象  

<table>
   <tr>
      <td>参数</td>
      <td>类型</td>
      <td>描述</td>
   </tr>
   <tr>
      <td>loginid</td>
      <td>String</td>
      <td>评论用户ID</td>
   </tr>
   <tr>
      <td>starnumber</td>
      <td>String</td>
      <td>评价星个数</td>
   </tr>
   <tr>
      <td>commentinfo</td>
      <td>String</td>
      <td>评论内容</td>
   </tr>
   <tr>
      <td>commenttime</td>
      <td>String</td>
      <td>评论时间</td>
   </tr>
</table>  

响应体示例：  

```javascript
{
    "commentinfos": [
        {
            "commentinfo": "中级护师",
            "commenttime": "2016-12-20 15:29:59",
            "loginid": "halee",
            "starnumber": "5"
        },
        {
            "commentinfo": "中级护师",
            "commenttime": "2016-12-20 15:30:43",
            "loginid": "marlie",
            "starnumber": "4"
        }
    ],
    "errcode": "0",
    "errmsg": "获取应用评价成功",
    "hasmore": 0,
    "starnumber": " 4.5"
}
```

<h2 id="cid_15">/api/app/appevaluation：应用使用评价请求</h2>  

<h3 id="cid_15_0">说明</h3>  

该请求由应用客户端向EMP管理端发起，用于终端用户上传应用使用评价。  

<h3 id="cid_15_1">URL</h3>  

http://ip:port/api/app/appevaluation?access_token=xxx  

说明：参数【access_token】 类型【String】 必选【是】 描述【访问接口凭证,通过URL参数携带】  

<h3 id="cid_15_2">HTTP请求方式</h3>  

POST  

<h3 id="cid_15_3">请求参数</h3>  

请求：appEvaluationReq  

<table>
   <tr>
      <td>参数</td>
      <td>类型</td>
      <td>必选</td>
      <td>描述</td>
   </tr>
   <tr>
      <td>version</td>
      <td>String</td>
      <td>否</td>
      <td>协议版本；首次定义，默认1.0</td>
   </tr>
   <tr>
      <td>appid</td>
      <td>String</td>
      <td>是</td>
      <td>应用编号</td>
   </tr>
   <tr>
      <td>apptype</td>
      <td>String</td>
      <td>是</td>
      <td>应用类型，1：Android应用，2：iOS应用（企业证书），3：iOS Appstore中的应用4：HTML5Web app应用，5：ExMobi应用</td>
   </tr>
   <tr>
      <td>appname</td>
      <td>String</td>
      <td>是</td>
      <td>应用名称</td>
   </tr>
   <tr>
      <td>appversion</td>
      <td>String</td>
      <td>是</td>
      <td>应用版本</td>
   </tr>
   <tr>
      <td>starnumber</td>
      <td>String</td>
      <td>是</td>
      <td>评价星个数</td>
   </tr>
   <tr>
      <td>message</td>
      <td>String</td>
      <td>否</td>
      <td>建议内容</td>
   </tr>
</table>  

请求体示例：  

```javascript
{
    "appid":"cn.com.fiberhome.nj.mapclient.GAEA",
    "apptype":"2",
    "appversion":"5.13.0",
    "appname":"Exmobi",
    "starnumber":"5",
    "message":"中级护师",
   "useraccount":"halee",
    "version": "3.0"
}
```

<h3 id="cid_15_4">返回数据</h3>  

输出：appEvaluationRsp  

<table>
   <tr>
      <td>参数</td>
      <td>类型</td>
      <td>描述</td>
   </tr>
   <tr>
      <td>errcode</td>
      <td>int</td>
      <td>0：成功；-1：失败</td>
   </tr>
   <tr>
      <td>errmsg</td>
      <td>String</td>
      <td>对返回码的文本描述内容</td>
   </tr>
</table>  

响应体示例：  

```javascript
{
    "errcode": "0",
    "errmsg": "上传应用评价成功"
}
```  

<h2 id="cid_16">/api/app/startimage：应用启动图片</h2>  

<h3 id="cid_16_0">说明</h3>  

定义启动图片API，用于支持应用在启动时，首屏显示的图片，应用在启动时，访问该API，获取到图片并展示。 

<h3 id="cid_16_1">URL</h3>  

http://ip:port/api/app/startimage?access_token=xxx    

说明：参数【access_token】 类型【String】 必选【是】 描述【访问接口凭证,通过URL参数携带】  

<h3 id="cid_16_2">HTTP请求方式</h3>  

GET  

<h3 id="cid_16_3">请求参数</h3>  

<table>
   <tr>
      <td>参数</td>
      <td>类型</td>
      <td>必选</td>
      <td>描述</td>
   </tr>
   <tr>
      <td>version</td>
      <td>String</td>
      <td>否</td>
      <td>协议版本；首次定义，默认1.0</td>
   </tr>
   <tr>
      <td>appid</td>
      <td>String</td>
      <td>是</td>
      <td>应用标识<br/>取值参考：应用管理页面中的应用标识信息</td>
   </tr>
   <tr>
      <td>clientid</td>
      <td>String</td>
      <td>否</td>
      <td>ExMobi应用在EDN打包产生的clientid值<br/>ExMobi应用时，该字段必选，其他类型可选<br/>取值参考：ExMobi应用的“EDN包管理”页面中客户端ID信息</td>
   </tr>
   <tr>
      <td>dpi</td>
      <td>String</td>
      <td>否</td>
      <td>手机屏幕密度，包含ldpi/mdpi/hdpi/xhdpi 四种，分别代表低分屏，中分屏，高分屏，超高分屏</td>
   </tr>
</table>

<h3 id="cid_16_4">返回数据</h3>  

<table>
   <tr>
      <td>参数</td>
      <td>类型</td>
      <td>描述</td>
   </tr>
   <tr>
      <td>errcode</td>
      <td>int</td>
      <td>0：成功；1:无启动图片</td>
   </tr>
   <tr>
      <td>errmsg</td>
      <td>String</td>
      <td>对返回码的文本描述内容</td>
   </tr>
   <tr>
      <td>id</td>
      <td>String</td>
      <td>图片ID</td>
   </tr>
   <tr>
      <td>starttime</td>
      <td>String</td>
      <td>图片有效期开始时间</td>
   </tr>
   <tr>
      <td>endtime</td>
      <td>String</td>
      <td>图片有效期结束时间</td>
   </tr>
   <tr>
      <td>url</td>
      <td>String</td>
      <td>图片的相对路径</td>
   </tr>
</table>  

响应体示例：  

Json数据，返回启动通知内容  

```javascript
{
       "errcode": "0",
       "errmsg": "成功",
       "id": "6025c1ef-0fc3-4460-8f41-4426346c369d",
       "starttime": "2016-11-21",
       "endtime": "2016-11-25",
       "url": "images/clienthomeimage/201611/003b6bf0-a0de-4b2d-b45f-e4d8ca788e4d.jpg",
 }
```  

Json数据，无启动图片  

```javascript
{
       "errcode": "1",
       "errmsg": "无启动图片"
 }
```  

<h2 id="cid_17">/api/app/startnotification：应用启动通知消息</h2>  

<h3 id="cid_17_0">说明</h3>  

定义启动通知API，用于支持应用在启动时，弹出的通知消息，应用在启动时，访问该API，获取到通知内容并展示。    

<h3 id="cid_17_1">URL</h3>  

http://ip:port/api/app/startnotification?access_token=xxx    

说明：参数【access_token】 类型【String】 必选【是】 描述【访问接口凭证,通过URL参数携带】  

<h3 id="cid_17_2">HTTP请求方式</h3>  

GET  

<h3 id="cid_17_3">请求参数</h3>  

<table>
   <tr>
      <td>参数</td>
      <td>类型</td>
      <td>必选</td>
      <td>描述</td>
   </tr>
   <tr>
      <td>version</td>
      <td>String</td>
      <td>否</td>
      <td>协议版本；首次定义，默认1.0</td>
   </tr>
   <tr>
      <td>appid</td>
      <td>String</td>
      <td>是</td>
      <td>应用标识<br/>取值参考：应用管理中的应用标识信息</td>
   </tr>
   <tr>
      <td>clientid</td>
      <td>String</td>
      <td>否 </td>
      <td>ExMobi应用在EDN打包产生的clientid值<br/><font color="red">ExMobi应用时，该字段必选，其他类型可选</font><br/>取值参考：ExMobi应用的“EDN包管理”页面中客户端ID信息</td>
   </tr>
</table>

<h3 id="cid_17_4">返回数据</h3>  

<table>
   <tr>
      <td>参数</td>
      <td>类型</td>
      <td>描述</td>
   </tr>
   <tr>
      <td>errcode</td>
      <td>int</td>
      <td>0：成功；-1：失败</td>
   </tr>
   <tr>
      <td>errmsg</td>
      <td>String</td>
      <td>对返回码的文本描述内容</td>
   </tr>
   <tr>
      <td>content</td>
      <td>String</td>
      <td>通知内容</td>
   </tr>
</table>  

Json数据，返回启动通知内容

```javascript
{
       "errcode": "0",
       "errmsg": "成功",
       "content": "通知内容"
 }
```

Json数据，无通知图片  

```javascript
{
       "errcode": "1",
       "errmsg": "无通知内容"
 }
```  

<h2 id="cid_18">/api/app/paramconfig：应用参数配置</h2>  

<h3 id="cid_18_0">说明</h3>  

定义应用配置参数API，用于支持应用动态获取运行的配置参数值，实现所有用户的应用的运行参数可以通过管理端远程修改。   

<h3 id="cid_18_1">URL</h3>  

http://ip:port/api/app/paramconfig?access_token=xxx  

说明：参数【access_token】 类型【String】 必选【是】 描述【访问接口凭证,通过URL参数携带】  

<h3 id="cid_18_2">HTTP请求方式</h3>  

GET  

<h3 id="cid_18_3">请求参数</h3>  

<table>
   <tr>
      <td>参数</td>
      <td>类型</td>
      <td>必选</td>
      <td>描述</td>
   </tr>
   <tr>
      <td>version</td>
      <td>String</td>
      <td>否</td>
      <td>协议版本；首次定义，默认1.0</td>
   </tr>
   <tr>
      <td>appid</td>
      <td>String</td>
      <td>是</td>
      <td>应用标识<br/>取值参考：应用管理中的应用标识信息</td>
   </tr>
</table>

<h3 id="cid_18_4">返回数据</h3>  

<table>
   <tr>
      <td>参数</td>
      <td>类型</td>
      <td>描述</td>
   </tr>
   <tr>
      <td>errcode</td>
      <td>int</td>
      <td>0：成功；-1：失败</td>
   </tr>
   <tr>
      <td>errmsg</td>
      <td>String</td>
      <td>对返回码的文本描述内容</td>
   </tr>
   <tr>
      <td>keyname</td>
      <td>String</td>
      <td>任意key名称，根据实际参数确定</td>
   </tr>
</table>  

Json数据，返回启动通知内容  

```javascript
{
       "result": "0",
       "pnsurl": "http://www.mydomain.com:8001/pns",
       "pnstcpport": "8002"
 }
```  

<h2 id="cid_19">/sso：sso校验接口</h2>  

<h3 id="cid_19_0">说明</h3>  

该请求由服务或第三方业务系统向EMP发起，用于校验sso_token是否有效。    

<h3 id="cid_19_1">URL</h3>  

http://ip:port/sso?sso_token=xxx   

说明：参数【access_token】 类型【String】 必选【是】 描述【访问接口凭证,通过URL参数携带】  

<h3 id="cid_19_2">HTTP请求方式</h3>  

GET  

<h3 id="cid_19_3">请求参数</h3>  

<table>
   <tr>
      <td>参数</td>
      <td>类型</td>
      <td>可选</td>
      <td>描述</td>
   </tr>
   <tr>
      <td>sso_token</td>
      <td>String</td>
      <td>否</td>
      <td>sso凭证</td>
   </tr>
</table>

<h3 id="cid_19_4">返回数据</h3>  

<table>
   <tr>
      <td>参数</td>
      <td>类型</td>
      <td>描述</td>
   </tr>
   <tr>
      <td>errcode</td>
      <td>int</td>
      <td>0：token有效<br/>其他参照错误访问码8300~8311</td>
   </tr>
   <tr>
      <td>errmsg</td>
      <td>String</td>
      <td>对返回码的文本描述内容</td>
   </tr>
   <tr>
      <td>sso_token</td>
      <td>String</td>
      <td>sso凭证</td>
   </tr>
   <tr>
      <td>expireTime</td>
      <td>String</td>
      <td>超期时间</td>
   </tr>
   <tr>
      <td>account</td>
      <td>String</td>
      <td>登录账号</td>
   </tr>
</table>



