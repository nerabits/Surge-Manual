# 配置文件版本

为获得更好的向后兼容性，从 Surge iOS 4.9.3 和 Surge Mac 4.2.2 开始，配置文件支持版本注释。

例如:
```
[Script]
panel = script-path=panel.js,type=generic 
```

注意：旧版本的 Surge 不支持 generic 类型的脚本声明。在旧版本配置脚本声明时，声明行会发生一个配置文件解析错误。

```
[Script]
#!PROFILE-VERSION-REQUIRED 10 panel = script-path=panel.js,type=generic 
```

可通过添加配置文件的版本注释解决。添加后，旧版本解析配置时会将这一行当作注释而忽略。

*请注意，该功能针对配置文件的分发而设计，例如 Managed Profile（托管配置）和 Enterprice Profile（企业配置）。当配置文件被用户使用 UI 修改时，所有的配置文件版本注释将被删除。*

## 配置文件版本更新日志

### 版本 0 (Surge iOS 4.9.3 和 Surge Mac 4.2.2 之前的全部版本)

### 版本 10 (Surge iOS 4.9.3 和 Surge Mac 4.2.2 之后的全部版本)

- 支持脚本类型 'generic'。
- 支持新的配置文件章节 [Panel]。 (Surge 不会解析未知的配置文件章节，因此不需要声明配置文件版本)

### 版本 11 (Surge iOS 4.11.0 和 Surge Mac 4.4.0 之后的全部版本)

- 支持 WireGuard 策略。

