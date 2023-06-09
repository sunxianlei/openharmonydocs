# 设备管理开发常见问题

## 如何获取设备的dpi值

适用于：OpenHarmony 3.2 Beta5，API9 Stage模型

**问题现象**

获取设备的dpi信息。

**解决措施**

导入@ohos.display包，通过getDefaultDisplaySync方法获取。

**示例代码**
  
```
import display from '@ohos.display'; 
let displayClass = null;
try {
    displayClass = display.getDefaultDisplaySync();
 console.info('Test densityDPI:' + JSON.stringify(data.densityDPI)); 
} catch (exception) {
    console.error('Failed to obtain the default display object. Code: ' + JSON.stringify(exception));
} 
```

## 如何获取当前运行设备类型

适用于：OpenHarmony SDK 3.2.2.5版本，API9 Stage模型

导入\@ohos.deviceInfo包，然后通过deviceInfo.deviceType获取设备类型。

参考文档：[设备信息](../reference/apis/js-apis-device-info.md)

## 如何获取设备系统版本

适用于：OpenHarmony SDK 3.2.5.5版本，API9 Stage模型

通过[deviceInfo](../reference/apis/js-apis-device-info.md)对象的osFullName属性获取设备系统版本。

## OpenHarmony设备如何获取UDID？

适用于：OpenHarmony SDK3.0, API9 Stage模型

1. 如果想获取连接设备的udid，可使用 hdc shell bm get --udid命令；

2. 如果想在代码中获得，参考文档 [udid](../reference/apis/js-apis-device-info.md) 。

## 开发快捷键功能

适用于：OpenHarmony SDK 3.2.6.5版本，API9 Stage模型

快捷键功能开发请使用组合按键api，具体可参考[组合按键（InputConsumer）](../reference/apis/js-apis-inputconsumer.md)
