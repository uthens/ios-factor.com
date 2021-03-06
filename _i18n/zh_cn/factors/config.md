应用配置应该是两次部署（App Store，TestFlight，开发环境）之间仅有的变化部分，或者是随着时间推移而不随着底层代码而改变的部分。它包括：

- 后台服务 API 的 key（无论是对内还是对外服务）；
- 远程资源的 URL（即应用使用的 API）；
- 功能开关。

应用配置有时候在代码中使用常量保存，这与 iOS-factor 的要求相违背。我们认为**配置与代码需要严格分离。**每次部署可能会更改配置部分，但代码部分则应完全一致。

判断一个应用的配置是否正确地独立于代码，一个简单的方法是看该应用的基准代码是否可以立刻开源，而不用担心暴露任何敏感信息。

在编译期注入配置的手段有很多种

- 使用配置文件（如JSON、YAML）；
- 使用 [cocoapods-keys](https://github.com/orta/cocoapods-keys) 可以更好隐藏键，并在 iOS 应用的编译期使用；
- 自定义的编译方案（如使用 build phase）。

iOS 平台的部署周期明显要长于服务器的部署周期，所以你可能想用 OTA 的方式对配置进行更新，以对问题进行快速响应。

通过 OTA 更新配置非常强大，并且可以让你立即完成以下事情：

- 开启特定的功能运行 A/B 测试，或者仅对一部分活跃用户进行一些 UI 上的改变；
- 轮换使用 API key；
- 更新网站主机地址或者其它已经改变的 URL；
- 远程关闭功能或者隐藏按钮。

如果没有 OTA 升级，则需要等待应用通过审核上架后才能见效。而每次提交审核都增加了被拒的风险，并潜在影响紧急版本的发布。

同时，应用也应具备后向兼容性，因为那些不能升级到最新 iOS 系统版本的用户可能压根就无法更新应用。通过提供 OTA 更新，你可以持续为应用的较老版本提供支持。

实现 OTA 更新配置的一些可能的方案：

- 使用自己的方案；
- 专用的 web 服务例如 [Firebase remote config](https://firebase.google.com/docs/remote-config/)。

