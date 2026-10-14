# HS5 Android环境探测器

这是一个不依赖第三方库的轻量Android探测APK，面向红旗HS5 Android 9车机。

它同时检查标准Android网络环境和车机的 Android 虚拟ACRN系统候选路径。



## 1 探测范围

- 只读检查 `WifiManager`、`WifiP2pManager`、系统特性、权限和全部网络接口；
- 查询 `com.faw.hqzl3.hqvehicleservice.HQVehicleService` 是否存在、启用、导出及其权限；
- 用户点击后尝试绑定上述服务，记录Binder类名和接口描述符，随后自动解绑；
- 在车机的18080端口启动HTTP自检页，列出所有可供iPhone访问的IPv4地址；
- 保留标准 `LocalOnlyHotspot` 测试作为对照项，它失败不代表T‑BOX 方案失败。
- 默认检测完全只读。“主动测试本地热点”按钮才会尝试创建热点，成功后8秒自动关闭。

本版本不会调用 `openAP()`。

在Binder接口、参数、权限和关闭方法得到实车确认前，不猜测原厂事务编号。



## 2 报告位置

点击“保存报告”后，通常写入：

```text
/sdcard/Android/data/com.kruse7do.hs5probe/files/reports/
```

报告会直接显示在屏幕上，即使车机文件管理器无法进入上述目录，也可以拍照记录关键结果。

重点关注：

- `WIFI_SERVICE class`
- `WifiManager unavailable`
- `WIFI_P2P_SERVICE class`
- `LocalOnlyHotspot API present`
- 主动测试后的 `ACTIVE RESULT`
- `Network interfaces`
- `FAW T-BOX candidate service`
- `T-BOX BIND RESULT`
- `T-BOX binder descriptor`
- `HTTP HIT`



## 3 本地编译

项目要求JDK 17、Android SDK 35和Gradle 8.9。

可以直接用Android Studio打开，也可以在命令行执行：

```text
gradle :app:assembleDebug
```
