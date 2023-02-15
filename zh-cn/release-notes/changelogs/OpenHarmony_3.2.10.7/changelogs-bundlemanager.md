# 包管理子系统ChangeLog

## cl.bundlemanager.1 包管理删除@ohos.bundle.bundleManager.d.ts中的getAbilityIcon接口，可以使用@ohos.resourceManager.d.ts中的getMediaContent替换。

包管理删除[@ohos.bundle.bundleManager.d.ts](https://gitee.com/openharmony/interface_sdk-js/blob/master/api/@ohos.bundle.bundleManager.d.ts)中的getAbilityIcon接口，可以使用[@ohos.resourceManager.d.ts](https://gitee.com/openharmony/interface_sdk-js/blob/master/api/@ohos.resourceManager.d.ts)中的getMediaContent替换。

**变更影响**<br>
使用之前已发布的API 9各beta版本且使用到了getAbilityIcon接口的，需要改为使用getMediaContent接口。

**关键的接口/组件变更**<br>
删除@ohos.bundle.bundleManager.d.ts中的getAbilityIcon接口。

**适配指导**<br>
使用@ohos.bundle.bundleManager.d.ts下面的getAbilityIcon，需要修改为@ohos.resourceManager.d.ts中的getMediaContent。需要提前获取到图标的资源ID值，可参考该接口的[使用指导](../../../application-dev/reference/apis/js-apis-resource-manager.md#getmediacontent9)。

## cl.bundlemanager.2 包管理底层能力变更，仅支持系统资源HAP自定义权限，其它HAP均不支持自定义权限。

仅支持系统资源HAP自定义权限，其它HAP均不支持自定义权限。包管理在解析HAP时，仅支持解析资源HAP(包名为：ohos.global.systemres)的配置文件中的definePermissions字段，该字段用来定义权限。其它HAP中配置的definePermissions字段将不会解析。
如果有应用需要自定义权限，可以在资源HAP的[配置文件](https://gitee.com/openharmony/utils_system_resources/blob/master/systemres/main/config.json)中definePermissions字段下面新增定义权限。格式可参考[定义权限](../../../application-dev/quick-start/module-structure.md#definepermissions对象内部结构)。


**变更影响**<br>
升级新版本镜像后，应用自定义的权限将不会生效，使用方在申请该权限时，会授权失败。

**关键的接口/组件变更**<br>
包管理底层能力变更，仅支持系统资源HAP自定义权限，其它HAP均不支持自定义权限。

**适配指导**<br>
如果有应用需要自定义权限，可以在资源HAP的[配置文件](https://gitee.com/openharmony/utils_system_resources/blob/master/systemres/main/config.json)中definePermissions字段下面新增定义权限。格式可参考[定义权限](../../../application-dev/quick-start/module-structure.md#definepermissions对象内部结构)。

## cl.bundlemanager.3 包管理二级模块文件名称变更，修改为文件内对应的接口名称

包管理二级模块文件名称变更，修改为文件内对应的接口名称，变更文件如下：

| 原文件名称 |变更后文件名称 |
|----|----|
| bundleManager/abilityInfo.d.ts |  bundleManager/AbilityInfo.d.ts |
| bundleManager/applicationInfo.d.ts |  bundleManager/ApplicationInfo.d.ts |
| bundleManager/bundleInfo.d.ts |  bundleManager/BundleInfo.d.ts |
| bundleManager/dispatchInfo.d.ts |  bundleManager/DispatchInfo.d.ts |
| bundleManager/elementName.d.ts |  bundleManager/ElementName.d.ts |
| bundleManager/extensionAbilityInfo.d.ts |  bundleManager/ExtensionAbilityInfo.d.ts |
| bundleManager/hapModuleInfo.d.ts |  bundleManager/HapModuleInfo.d.ts |
| bundleManager/launcherAbilityInfo.d.ts |  bundleManager/LauncherAbilityInfo.d.ts |
| bundleManager/metadata.d.ts |  bundleManager/Metadata.d.ts |
| bundleManager/packInfo.d.ts |  bundleManager/BundlePackInfo.d.ts |
| bundleManager/permissionDef.d.ts |  bundleManager/PermissionDef.d.ts |
| bundleManager/remoteAbilityInfo.d.ts |  bundleManager/RemoteAbilityInfo.d.ts |
| bundleManager/shortcutInfo.d.ts |  bundleManager/ShortcutInfo.d.ts |

除了免安装相关的BundlePackInfo文件名称增加了Bundle，其余文件名称均是修改为大写开头。

**变更影响**<br>
仅修改二级模块文件名称，不会影响一级模块的使用。在使用之前已发布的API 9各beta版本时，如果在ts文件中直接导入了bundleManager下面二级模块接口的，IDE中编译报错的话，需要修改导入的文件名称。

**关键的接口/组件变更**<br>
变更bundleManager文件夹下面的d.ts名称，修改为文件中的接口名称。

**适配指导**<br>
使用新的sdk后，正常情况下应用无需适配该变更。如果在应用中直接导入了bundleManager文件夹下面的文件，则需要修改导入的文件名称。可以按照如下的修改方式：

**修改前：**
```ts
import {AbilityInfo} from 'bundleManger/abilityInfo';
import {ExtensionAbilityInfo} from 'bundleManger/extensionAbilityInfo';
import {BundlePackInfo} from 'bundleManger/packInfo';
```
**修改后：**
```ts
import {AbilityInfo} from 'bundleManger/AbilityInfo';
import {ExtensionAbilityInfo} from 'bundleManger/ExtensionAbilityInfo';
import {BundlePackInfo} from 'bundleManger/BundlePackInfo';
```