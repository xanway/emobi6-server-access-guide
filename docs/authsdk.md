# 微服务鉴权SDK集成  

----------

<h2 id="cid_0">Android集成</h2>  

<h3 id="cid_0_0">兼容性</h3>  

支持Android2.3及以上系统。  

<h3 id="cid_0_1">导入access-sdk.jar</h3>  

SDK下载地址[ExMobi6微服务鉴权AndroidSDK](https://www.exmobi.cn/resource/download/info/f8e92360-1e8d-11e7-8b84-470cb0530024.do)。  

<h3 id="cid_0_2">配置AndroidManifest.xml</h3>  

```xml
<manifest……>
<application ……>
    ……
<activity ……/>
</application>
<uses-sdk android:minSdkVersion="8"></uses-sdk>
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"></uses-permission>
<uses-permission android:name="android.permission.INTERNET"></uses-permission>
<uses-permission android:name="android.permission.READ_PHONE_STATE"></uses-permission>
</manifest>
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"></uses-permission>
</manifest>
```

说明：  

<table>
   <tr>
      <td>权限</td>
      <td>用途</td>
   </tr>
   <tr>
      <td>INTERNET(必须)</td>
      <td>允许应用程序联网，以便向我们的服务器端发送数据。</td>
   </tr>
   <tr>
      <td>READ_PHONE_STATE(必须)</td>
      <td>获取用户手机的IMEI，用来唯一的标识用户。</td>
   </tr>
   <tr>
      <td>ACCESS_NETWORK_STATE(必须)</td>
      <td>检测网络状态。</td>
   </tr>
   <tr>
      <td>WRITE_EXTERNAL_STORAGE(必须)</td>
      <td>允许程序写入外部存储，如SD卡上写文件</td>
   </tr>
</table>

<h3 id="cid_0_3">接口调用</h3>  

1.代码中引入API接口类  

```java
import com.fiberhome.exmobi.AccessAgent;
import com.fiberhome.exmobi.OnAccessListener;
```

2.在程序启动后需要先调用AccessAgent.init(accessCode)方法，初始化SDK配置信息；    

3.从ExMobi管理平台申请访问码accessCode及服务器地址url，调用AccessAgent.getToken(url, onAccessListener)方法；  

4.onAccessListener监听类回调函数中获取状态，若获取成功则返回token值及超时时间，若获取失败则返回错误状态码；  

5.获取token后，根据服务商提供接口定义获取服务结果；  

6.若需重置配置，则可调用AccessAgent.init(accessCode)方法实现；  

<h3 id="cid_0_4">API接口定义</h3>  

<h4 id="cid_0_4_0">com.fiberhome.exmobi.OnAccessListener</h4>  

OnAccessListener接口类用于从ExMobi服务器获取token值回调，使用时候需要实现OnAccessListener接口类，或构建匿名接口类。  

<table>
   <tr>
      <td>方法名</td>
      <td>描述</td>
   </tr>
   <tr>
      <td>void onResult (int code,String token,String expiresIn)</td>
      <td>操作成功回调<br/>参数：code：回应状态码，数字枚举型 [0,1,2,3,4] <br/>0成功 <br/>1访问码不存在<br/>2应用包不存在<br/>3鉴权失败<br/>4系统异常<br/><br/>token：服务器回应token码，字符串类型，成功时生效,失败则返回null<br/>expiresIn：凭证的有效时间（秒），字符串类型，成功时生效，获取失败返回null</td>
   </tr>
</table>

<h4 id="cid_0_4_1">com.fiberhome.exmobi. AccessAgent</h4>  

AccessAgent类用于从ExMobi服务器获取token值，该方法为异步方法，token值通过回调监听获取。  

<table>
   <tr>
      <td>方法名</td>
      <td>描述</td>
   </tr>
   <tr>
      <td>void  init(Context context,String accessCode,String appId)</td>
      <td>初始化ExMobi鉴权SDK<br/>参数：<br/>context：第三方应用上下文环境，Contex类型，必选项；<br/>accessCode：从ExMobi管理平台申请的访问码，字符串类型，必选项；<br/>appId：应用插件id，字符串类型，可选项；<br/>注：第三方集成时候appId不填写</td>
   </tr>
   <tr>
      <td>void  getToken(Context context,String url,OnAccessListener ,onAccessListener)</td>
      <td>ExMobi SDK获取指定服务token值<br/>参数：<br/>context：第三方应用上下文环境，Contex类型，必选项；<br/>url：查询服务器地址，支持http和https请求，字符串类型，必选项；<br/>onAccessListener：获取token结果回调监听，成功或失败均会进入类onResult回调函数中；</td>
   </tr>
</table>  

<h2 id="cid_1">Ios集成</h2>  

<h3 id="cid_1_0">兼容性</h3>  

支持IOS 7.0及以上系统  

<h3 id="cid_1_1">导入exmobi6.framework（简称SDK）</h3>  

SDK下载地址：[ExMobi6微服务鉴权IosSDK](https://www.exmobi.cn/resource/download/info/414d3e20-1e8e-11e7-8b84-470cb0530024.do)  

1.将SDK目录下exmobi6.framework拖入工程。默认情况下XCode会自动添加引用。如果有引用问题，可以在Build Settings->Framework Search Paths中添加对应路径。  

2.将SDK目录下CSAgent文件夹下的依赖文件加入工程。CSAgent目录下包含以下两个目录文件
AFNetworking文件为3.0版本。ExMobiRsa为先维内部共享库，该目录下的Libcrypto.a与libssl.a为openssl标准库。  

<h3 id="cid_1_2">接口调用</h3>  

1.代码中引入API类

```C++
import  <exmobi6/exmobi6.h>
```


2.在程序启动后需要先调用[exmobi6 init:accessCode]方法，初始化SDK配置信息  

3.从ExMobi管理平台申请访问码accessCode及服务器地址url，调用[exmobi6 getToken:@" IP:port" onCsgListener:^(int code, NSString *token,NSString *message) {}方法；  

4.onCsgListener Block中获取状态，若获取成功则返回token值及超时时间，若获取失败则返回错误状态码；  

5.获取token后，根据服务商提供接口定义获取服务结果；  

6.若需重置配置，则可调用[exmobi6 init:accessCode]方法实现；  

<h3 id="cid_1_3">Demo工程</h3>  

见SDK压缩包下demo目录下示例工程。  

<h3 id="cid_1_4">API接口定义</h3>  

<h4 id="cid_1_4_0">onCsgListener</h4>  

onCsgListener类用于从ExMobi服务器获取token值，该方法为异步方法，token值通过回调监听获取。  

<table>
   <tr>
      <td>方法名</td>
      <td>描述</td>
   </tr>
   <tr>
      <td>onCsgListener (int code,String token,String expiresIn)</td>
      <td>操作成功回调<br/>参数：<br/>code：回应状态码，数字枚举型 [0,1,2,3,4] <br/>0成功 <br/>1访问码不存在<br/>2应用包不存在<br/>3鉴权失败<br/>4系统异常<br/>token：服务器回应token码，字符串类型，成功时生效,失败则返回null<br/>expiresIn：凭证的有效时间（秒），字符串类型，成功时生效，获取失败返回null</td>
   </tr>
</table>