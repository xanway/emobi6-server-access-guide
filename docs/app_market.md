# 应用超市开发

----------

平台提供了支持应用超市的开发接口，相关接口参照[ExMobi-server6.x平台接口定义章节](https://gitdocument.exmobi.cn/exmobi6-server-access-guide/access_define.html)。  

ExMobi应用在开发过程中快捷的实现应用超市的功能，只需要在页面中使用工具类**AppUtil.setSettingInfo**脚本进行初始化和appworkbench工作台控件即可。  

示例代码如下：

```html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.1//EN" "http://www.nj.fiberhome.com.cn/exmobi.dtd">
<html>
	<head>
		<title show="false"/>
		<script type="text/javascript">
          //设置应用超市服务器地址
			<![CDATA[
				var settingInfoJson= {};
				settingInfoJson.url= "http://192.168.160.159:8090/";
				AppUtil.setSettingInfo(settingInfoJson);
			]]>
		</script>
	</head> 
	<body style="background-color:white;padding:0 10;">
<appworkbench id="exmobi"/>
	</body>
</html>

```   

如需自定义应用超市，开发者可以调用相关接口获取数据进行页面组装。 
