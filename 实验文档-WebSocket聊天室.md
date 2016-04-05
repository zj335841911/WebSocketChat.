# Java和WebSocket开发网页即时聊天室 #

----------


# 一、项目说明及简介 #

### 1. 项目简介 ###

WebSocket 是HTML5一种新的协议，它实现了浏览器与服务器全双工通信，这里就将使用WebSocket来开发网页聊天室，前端框架会使用AmazeUI，后台使用Java，编辑器使用UMEditor。

### 2. 涉及知识点 ###

	网页前端（HTML5 + CSS3 + JS）和 JavaEE。

### 3. 软件环境 ###
	
	Tomcat8
	JavaEE7
	JDK7
	Eclipse-JavaEE 或 MyEclipse
	支持HTML5的浏览器

### 4. 相关框架 ###

	jQuery—1.X
	妹子UI（AmazeUI-2.5.2）
	百度富文本编辑器（UMeditor1_2_2）


### 5. 源代码下载 ###




# 二、新建空项目 #

打开Eclipse JavaEE，新建一个名为Chat的Dynamic Web Project，

然后导入处理JSON格式字符串所需要的包，

	commons-beanutils-1.8.0.jar
	commons-collections-3.2.1.jar
	commons-lang-2.5.jar
	commons-logging-1.1.1.jar
	ezmorph-1.0.6.jar
	json-lib-2.4-jdk15.jar

把这几个包放在/WEB-INF/lib目录下，最后把项目发布到Tomcat8服务器上，到此空项目就搭建完成了。

Eclipse的默认项目根目录叫WebContent，
MyEclipse默认项目根目录叫WebRoot，

在本篇文档中，我们接下来用WebRoot作为项目根目录。


# 三、编写前端页面 #

这里使用了AmazeUI框架，它是一个跨屏自适应的前端框架

消息输入框使用了UMEditor，它是一个富文本在线编辑器，能让我们的消息内容多姿多彩。


在WebContent目录下新建一个名为index.jsp的页面，

首先从AmazeUI官网下载压缩包，然后解压把assets文件夹拷贝到WebRoot目录下，这样我们就能使用AmazeUI了。

再从UEditer官网下载Mini版的JSP版本压缩包，解压后把整个目录拷贝到WebRoot目录下，

接下来就可以编写前端代码了，代码如下（可按照自己的审美去编写）：

	<%@ page language="java" import="java.util.*" pageEncoding="UTF-8"%>
	<%
	String path = request.getContextPath();
	String basePath = request.getScheme()+"://"+request.getServerName()+":"+request.getServerPort()+path+"/";
	%>
	<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN">
	<html>
	<head>
		<meta charset="UTF-8">
		<title>Landing Page | Amaze UI Example</title>
		<meta http-equiv="X-UA-Compatible" content="IE=edge">
		<meta name="viewport" content="width=device-width, initial-scale=1">
		<meta name="format-detection" content="telephone=no">
		<meta name="renderer" content="webkit">
		<meta http-equiv="Cache-Control" content="no-siteapp"/>
		
		<script src="assets/js/jquery.min.js"></script>
		<!-- 妹子UI相关资源 -->
		<link rel="alternate icon" type="image/png" href="assets/i/favicon.png">
		<link rel="stylesheet" href="assets/css/amazeui.min.css"/>
		<script src="assets/js/amazeui.min.js"></script>
		<!-- UM相关资源 -->
		<link href="assets/umeditor/themes/default/css/umeditor.css" type="text/css" rel="stylesheet">
		<script type="text/javascript" charset="utf-8" src="assets/umeditor/umeditor.config.js"></script>
		<script type="text/javascript" charset="utf-8" src="assets/umeditor/umeditor.min.js"></script>
		<script type="text/javascript" src="assets/umeditor/lang/zh-cn/zh-cn.js"></script>
	</head>
	<body>
	<header class="am-topbar am-topbar-fixed-top">
	  <div class="am-container">
	    <h1 class="am-topbar-brand">
	      <a href="#">聊天室</a>
	    </h1>
	    <div class="am-collapse am-topbar-collapse" id="collapse-head">
	      <ul class="am-nav am-nav-pills am-topbar-nav">
	        <li class="am-active"><a href="#">首页</a></li>
	        <li><a href="#">项目</a></li>
	      </ul>
	
	      <div class="am-topbar-right">
	        <button class="am-btn am-btn-secondary am-topbar-btn am-btn-sm"><span class="am-icon-pencil"></span> 注册</button>
	      </div>
	
	      <div class="am-topbar-right">
	        <button class="am-btn am-btn-primary am-topbar-btn am-btn-sm"><span class="am-icon-user"></span> 登录</button>
	      </div>
	    </div>
	  </div>
	</header>
	
	<div id="main">
		<!-- 聊天内容展示区域 -->
		<div id="ChatBox" class="am-g am-g-fixed" >
		  <div class="am-u-lg-12" style="height:400px;border:1px solid #999;overflow-y:scroll;">
			<ul id="chatContent" class="am-comments-list am-comments-list-flip">
				<li class="am-comment am-comment-success" style="margin-right:20%;">
					<a href="">
						<img class="am-comment-avatar" src="assets/images/other.jpg" alt=""/>
					</a>
					<div class="am-comment-main" >
						<header class="am-comment-hd">
							<div class="am-comment-meta">
							  <a href="#link-to-user" class="am-comment-author">某人</a>
							  <time datetime="" title="">2014-7-12 15:30</time>
							</div>
						</header>
					 <div class="am-comment-bd">此处是消息内容</div>
					</div>
				</li>
				<li class="am-comment am-comment-flip am-comment-warning" style="margin-left:20%;">
					<a href="">
						<img class="am-comment-avatar" src="assets/images/xia.jpg" alt=""/>
					</a>
					<div class="am-comment-main" >
						<header class="am-comment-hd">
							<div class="am-comment-meta">
							  <a href="#link-to-user" class="am-comment-author">某人</a>
							  <time datetime="" title="">2014-7-12 15:30</time>
							</div>
						</header>
					 <div class="am-comment-bd">此处是消息内容</div>
					</div>
				</li>
			</ul>
		  </div>
		</div>
		<!-- 聊天内容发送区域 -->
		<div id="EditBox" class="am-g am-g-fixed">
		<!--style给定宽度可以影响编辑器的最终宽度-->
		<script type="text/plain" id="myEditor" style="width:100%;height:140px;"></script>
		<button id="send" type="button" class="am-btn am-btn-primary am-btn-block">发送</button>
		</div>
	  
	</div>
	
	<script type="text/javascript">
	$(function(){
		
		//窗口大小变化时，调整显示效果
		$("#ChatBox div:eq(0)").height($(this).height()-290);
		$(window).resize(function(){
			$("#ChatBox div:eq(0)").height($(this).height()-290);
		});
	
		//实例化编辑器
	    var um = UM.getEditor('myEditor',{
	    	initialContent:"请输入聊天信息...",
	    	autoHeightEnabled:false,
	    	toolbar:[
	            'source | undo redo | bold italic underline strikethrough | superscript subscript | forecolor backcolor | removeformat |',
	            'insertorderedlist insertunorderedlist | selectall cleardoc paragraph | fontfamily fontsize' ,
	            '| justifyleft justifycenter justifyright justifyjustify |',
	            'link unlink | emotion image video  | map'
	        ]
	    });
	
		
	});
	
	</script>
	
	</body>
	</html>


编写完成之后启动Tomcat服务器，然后访问index.jsp ，会看到设计好的页面效果。

上面的实例代码里有两条示例消息，一条别人的消息，一条自己的消息。


# 四、消息流转 #

聊天室的核心就是把一个人的消息广播给所有人，

我们这里使用WebSocket技术让所有人的浏览器都与服务器连在一起，

当一个人发送消息到服务器后，服务器把消息转发给所有人，包括自己，

这样每个人的浏览器就都能看到这条消息，

出现一条新消息时必备的3个属性：【发言人昵称】，【消息内容】和【发送时间】，

为了区别消息是否为自己，我们还需要在消息中加入一项属性：【是否自己】，

其中【发送时间】和【是否自己】可以由服务器进行处理，

那么发言人只需要告诉服务器【昵称】与【消息内容】即可：


	//浏览器发给服务器的数据：
	{
		nickname:"风清扬",
		content:"HelloWorld"
	}

	//浏览器接收的数据：
	{
		nickname:"风清扬",
		content:"HelloWorld",
		date:"2016.04.01 14:05:22",
		isSelf:true
	}


# 五、JS添加新消息 #

页面样式已经设计好，而真正聊天的时候肯定需要不断展示新的消息，

为了方便控制，我们使用JavaScript统一消息的创建过程。

页面中代表消息的li元素只保留一份，把它作为消息的模板，默认隐藏，

每当新消息到来，我们就复制一份模板，修改其中的属性，追加到列表中去展示，

给几个元素加上独有的标记：
【昵称】：ff="nickname"
【内容】：ff="content"
【时间】：ff="msgdate"

	<li id="msgtmp" class="am-comment" style="display:none;">
	    <a href="">
	        <img class="am-comment-avatar" src="assets/images/other.jpg" alt=""/>
	    </a>
	    <div class="am-comment-main" >
	        <header class="am-comment-hd">
	            <div class="am-comment-meta">
	              <a ff="nickname" href="#link-to-user" class="am-comment-author">某人</a>
	              <time ff="msgdate" datetime="" title="">2014-7-12 15:30</time>
	            </div>
	        </header>
	     <div ff="content" class="am-comment-bd">此处是消息内容</div>
	    </div>
	</li>


使用JS克隆一份模板，设置克隆体里面的数据，最终追加到列表中：


	//向聊天窗口加入一条消息
	function addMessage(msg){
	
		var box = $("#msgtmp").clone(); 	//复制一份模板，取名为box
		box.show();							//设置box状态为显示
		box.appendTo("#chatContent");		//把box追加到聊天面板中
		box.find('[ff="nickname"]').html(msg.nickname); //在box中设置昵称
		box.find('[ff="msgdate"]').html(msg.date); 		//在box中设置时间
		box.find('[ff="content"]').html(msg.content); 	//在box中设置内容
		box.addClass(msg.isSelf? 'am-comment-flip':'');	//右侧显示
		box.addClass(msg.isSelf? 'am-comment-warning':'am-comment-success');//颜色
		box.css((msg.isSelf? 'margin-left':'margin-right'),"20%");//外边距
		
		$("#ChatBox div:eq(0)").scrollTop(999999); 	//滚动条移动至最底部
	}

# 六、编写后台代码 #

新建一个com.zhenzhigu.chat的包，在包中创建一个名为ChatServer的类，

从JavaEE 7开始就统一了WebSocket的API，因此无论是什么服务器，用Java写的代码都是一样的，代码如下：

	
	package com.zhenzhigu.chat;
	
	import java.text.SimpleDateFormat;
	import java.util.Date;
	import java.util.Vector;
	
	import javax.websocket.OnClose;
	import javax.websocket.OnError;
	import javax.websocket.OnMessage;
	import javax.websocket.OnOpen;
	import javax.websocket.Session;
	import javax.websocket.server.ServerEndpoint;
	
	import net.sf.json.JSONObject;
	
	@ServerEndpoint("/websocket")
	public class ChatServer {
	
		private static SimpleDateFormat df = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
		private static Vector<Session> room = new Vector<Session>();
		
		/**
		 * 用户接入
		 * @param session 可选
		 */
		@OnOpen
		public void onOpen(Session session){
			room.addElement(session);
		}
		
		/**
		 * 接收到来自用户的消息
		 * @param message
		 * @param session
		 */
		@OnMessage
		public void onMessage(String message,Session session){
			//把用户发来的消息解析为JSON对象
			JSONObject obj = JSONObject.fromObject(message);
			//向JSON对象中添加发送时间
			obj.put("date", df.format(new Date()));
			//遍历聊天室中的所有会话
			for(Session se : room){
				//设置消息是否为自己的
				obj.put("isSelf", se.equals(session));
				//发送消息给远程用户
				se.getAsyncRemote().sendText(obj.toString());
			}
		}
		
		/**
		 * 用户断开
		 * @param session
		 */
		@OnClose
		public void onClose(Session session){
			room.remove(session);
		}
		
		/**
		 * 用户连接异常
		 * @param t
		 */
		@OnError
		public void onError(Throwable t){
			
		}
	}



# 七、前台、后台交互 #

后台写完了，前台要用WebSocket连接后台，需要新建一个WebSocket对象，然后就可以和服务器端进行交互，从浏览器发送消息给服务器端，同时要验证输入框的内容是否为空，然后接受服务端发送的消息，把它们动态地添加到聊天内容框中。

记得写到文档就绪函数中
	
	//自己的昵称
	var nickname = "风清扬"+Math.random();

	//建立一条与服务器之间的连接
	var socket = new WebSocket("ws://${pageContext.request.getServerName()}:${pageContext.request.getServerPort()}${pageContext.request.contextPath}/websocket");
    
	//接收服务器的消息
    socket.onmessage=function(ev){
    	var obj = eval(   '('+ev.data+')'   );
    	addMessage(obj)
    }

    //发送按钮被点击时
    $("#send").click(function(){
    	if (!um.hasContents()) {  // 判断消息输入框是否为空
            // 消息输入框获取焦点
            um.focus();
            // 添加抖动效果
            $('.edui-container').addClass('am-animation-shake');
            setTimeout("$('.edui-container').removeClass('am-animation-shake')", 1000);
        } else {
        	//获取输入框的内容
        	var txt = um.getContent();
        	//构建一个标准格式的JSON对象
        	var obj = JSON.stringify({
	    		nickname:nickname,
	    		content:txt
	    	});
            // 发送消息
            socket.send(obj);
            // 清空消息输入框
            um.setContent('');
            // 消息输入框获取焦点
            um.focus();
        }
    
    });

到这步，简单的网页聊天室就完成了，你可以多开几个窗口或在局域网中邀请小伙伴们来一起测试。

# 八、作业思考 #

本次项目课只是简单的实现聊天室，其实还有很多功能可以增加，例如头像上传功能、一对一聊天功能等，请考虑如何完善聊天室。

