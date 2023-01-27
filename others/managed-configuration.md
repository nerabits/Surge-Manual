# 托管配置

如果 Surge 配置文件开头为以下内容，Surge 可以从 URL 自动更新配置文件。

`#!MANAGED-CONFIG http://test.com/surge.conf interval=60 strict=true`

当且仅当 Surge 主程序运行时，才可自动更新配置文件。

> 注意：新的托管配置必须包含 #!MANAGED-CONFIG，否则 Surge 仍将视其为普通配置。

### 参数
   
#### interval: 可选，单位为秒 (默认: 86400秒).
用于配置更新配置文件的间隔时间。

#### strict: 可选值为 true 或 false (默认: false).

如果 strict 配置为 true，Surge 将会在每个周期开始时强制更新配置文件。当更新失败时，将会自动应用过时的配置文件。

> 注意：即使 strict 配置为 true，用户仍可以通过小组件和系统设置中的 VPN 开关开启 Surge。


