# arthas-plus
基于arthas和arthas-tunnel-server开发，在web页面查看arthas远程诊断java的信息

# 项目功能说明：
使用python开发，基于arthas和arthas-tunnel-server开发，包含文件和功能如下：
	• arthas_startup.py        #项目主程序.
		○ 自行判断并安装相应的独立环境和依赖包（miniconda、sanic等）
		○ 启动arthas tunnel server，退出后自动关闭arthas tunnel server。
		○ 自动判断和推送arthas客户端和启动脚本到服务器。
		○ 启动和关闭arthas客户端。
	• arthas_data.py        #数据包，包含远程服务器ip、启动arthas客户端用户、要监控的程序名。
	• start_arthas_client.sh   #arthas客户端启动脚本。
	• start_arthas.log   #日志文件
	• index.html         #主页，可以选择服务，并传参agentid到arthas tunnel server上。

# /opt/arthas目录：

├── arthas-agent.jar

├── arthas-boot.jar

├── arthas-client

│   ├── arthas-agent.jar

│   ├── arthas-boot.jar

│   ├── arthas-client.jar

│   ├── arthas-core.jar

│   ├── arthas.properties

│   ├── arthas-spy.jar

│   ├── as.bat

│   ├── as-service.bat

│   ├── as.sh

│   ├── async-profiler

│   ├── install-local.sh

│   ├── lib

│   ├── logback.xml

│   ├── math-game.jar

│   └── start_arthas_client.sh

├── arthas-client.jar

├── arthas-core.jar

├── arthas_data.py

├── arthas.properties

├── arthas-spy.jar

├── arthas_startup.py

├── arthas-tunnel-server-3.6.9-fatjar.jar

├── as.bat

├── as-service.bat

├── as.sh

├── async-profiler

│   ├── libasyncProfiler-linux-arm64.so

│   ├── libasyncProfiler-linux-musl-arm64.so

│   ├── libasyncProfiler-linux-musl-x64.so

│   ├── libasyncProfiler-linux-x64.so

│   └── libasyncProfiler-mac.so

├── index.html

├── install-local.sh

├── inventory.ini

├── lib

│   ├── libArthasJniLibrary-aarch64.so

│   ├── libArthasJniLibrary.dylib

│   ├── libArthasJniLibrary-x64.dll

│   └── libArthasJniLibrary-x64.so

├── logback.xml

├── math-game.jar

├── __pycache__

│   └── arthas_data.cpython-311.pyc

└── start_arthas.log


# 前提条件：
	• 启动arthas服务的服务端已和各客户端做过免密。
	• python需要3.9以上。
	• 安装必要依赖sanic。（启动程序会自动安装环境）
	• arthas tunnel server 版本为3.6.9。（3.7.1参数有变化，并加入验证。）
	https://github.com/alibaba/arthas/blob/master/tunnel-server/README.md
	• arthas tunnel server中的index.html有修改，是关于取参和自动刷新。
	• 需要修改arthas-tunnel-server的程序中的js，进行页面跳转传参。
	arthas-tunnel-server-3.6.9-fatjar.jar\BOOT-INF\classes\static\index.html
		
		增加js：
		
		<script>
		  document.addEventListener('DOMContentLoaded', function () {
		    // 判断 URL 是否包含 refresh 参数
		    const urlParams = new URLSearchParams(window.location.search);
		    if (urlParams.has('refresh') && urlParams.get('refresh') === 'true') {
		      // 移除 refresh 参数，并延时5秒后刷新页面
		      urlParams.delete('refresh');
		      const newURL = window.location.pathname + '?' + urlParams.toString();
		      setTimeout(function () {
		        window.location.replace(newURL);
		      }, 5000); // 等待5秒后刷新
		    }
		
		
		  <script>
		    // 获取 URL 参数
		    const params = new URLSearchParams(window.location.search);
		    // 获取 AgentId 参数的值
		    const agent = params.get('AgentId');
		    // 将 AgentId 的值填入输入框
		    document.getElementById('agentId').value = agent;
		  </script>
		


# 项目效果图：
主页面
<img width="957" height="797" alt="image" src="https://github.com/user-attachments/assets/e5e55c82-4fd6-43a6-af03-d1e45092064a" />
web快捷查看，自动访问远程服务。
<img width="968" height="531" alt="image" src="https://github.com/user-attachments/assets/01e302c2-d53f-4ca4-89b5-4ef26f1cc3e6" />
web快捷查看，具体java诊断信息。
<img width="956" height="536" alt="image" src="https://github.com/user-attachments/assets/ecb43243-1ca9-473b-ba84-ba2b4b9a2ba7" />
arthas-tunnel-server，自动跳转到待诊断的服务上。
<img width="1036" height="240" alt="image" src="https://github.com/user-attachments/assets/3b3e2aa0-2d59-4d1e-9494-58c6b815b89b" />





