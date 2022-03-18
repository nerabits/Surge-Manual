## Surge iOS 的 URL Scheme

Surge iOS 支持 4 种操作和 1 种参数。

操作：

* surge:///start 

  基于选中的配置文件启动。
  
* surge:///stop 

  停止当前应用会话。
  
* surge:///toggle

  基于选中的配置文件启动或停止。
  
* surge:///install-config?url=x

  从 URL 安装配置文件。URL 字段需要被转换为 URL 编码。

参数：

* autoclose=true

  操作完成时自动关闭 Surge。（不能与 install-config 一同使用）

  示例: surge:///toggle?autoclose=true
  
  
## x-callback-url

Surge 在 v3.4 版本开始支持 x-callback-url 规范。URL scheme 为 'surge'，可用的操作包含 'start'、'stop' 和 'toggle'。


