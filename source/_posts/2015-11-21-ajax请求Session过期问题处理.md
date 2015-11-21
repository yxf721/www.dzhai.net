title: Ajax请求Session过期问题处理
categories: Session
tags:
  - Session
  - jQuery
keywords: Ajax请求Session过期问题处理
date: 2015-11-21 15:59:43
---

当前解决方案重写jquery的$.ajax方法中的success、error、complete方法
当返回内容是501的时候 直接当前页面 跳转登录页面

如果需要自己处理ajax方法
在ajax中添加参数overrideDefault:true
![ajax](http://7xjq6x.com1.z0.glb.clouddn.com/20150924/ajax.png)

<!--more-->

```
//ajax 处理全局异常和session过期问题
var _overrideAjax = true;
(function overrideJQeuryAjax(){
	if(!_overrideAjax){
		return;
	}
	var oriAjax = $.ajax;
	// Override jquery ajax to check if session is valid.
	$.ajax = function(options) {
		var dataType = options.dataType;
		var overrideDefault=options.overrideDefault;
		if(typeof(overrideDefault)=='undefined'){
			overrideDefault=false;
		}
		var callback = options["callback"];
		var oriSuccess = options["success"];
		if ($.isFunction(oriSuccess)) {
			options["success"] = function(result) {
				if (!overrideDefault && !_checkSessionTimeout(result, dataType)) {
					//ajax session过期刷新当前页面
					window.location.href=window.location.href;
					return false;
				}
				oriSuccess(result);
			};
		}
		var oriComplete = options["complete"];
		if ($.isFunction(oriComplete)) {
			options["complete"] = function(xmlHttpRequest, textStatus) {
				var result = xmlHttpRequest.responseText;
				if (!overrideDefault && !_checkSessionTimeout(result, dataType)) {
					window.location.href=window.location.href;
					return false;
				}
				oriComplete(xmlHttpRequest, textStatus);
			};
		}
		
		//if error function is undefined, set default logic
		var orierror = options["error"];		
		if (!$.isFunction(orierror)) {
			options["error"] = function(err) {
				//alert("ERROR: "+err.status+" "+err.statusText);
				newCommon.lert("alway",{title:"温馨提示",del:true,content:'系统繁忙，请稍后重试'});
				//return false;
			};
		}		
		oriAjax(options);
	};
})();

function _checkSessionTimeout(result,dataType){
	var flag = true;	
	if(typeof(result)!='undefined' && result==501){
		flag = false;
	}
	return flag;
}
```


