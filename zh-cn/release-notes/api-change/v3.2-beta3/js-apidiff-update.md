# 升级服务子系统JS API变更

OpenHarmony 3.2 Beta3版本相较于OpenHarmony 3.2 Beta2版本，升级服务子系统的API变更如下:

## 接口变更

| 模块名 | 类名 | 方法/属性/枚举/常量 | 变更类型 |
|---|---|---|---|
| ohos.update | Order                | INSTALL_AND_APPLY = 6                                                                                                                                                                                                                                                                                                | 新增 |
| ohos.update | Order                | DOWNLOAD_AND_INSTALL = 3                                                                                                                                                                                                                                                                                             | 新增 |
| ohos.update | NetType              | CELLULAR_AND_WIFI = 7                                                                                                                                                                                                                                                                                                | 新增 |
| ohos.update | NetType              | WIFI = 6                                                                                                                                                                                                                                                                                                             | 新增 |
| ohos.update | DescriptionFormat    | SIMPLIFIED = 1                                                                                                                                                                                                                                                                                                       | 新增 |
| ohos.update | DescriptionFormat    | STANDARD = 0                                                                                                                                                                                                                                                                                                         | 新增 |
| ohos.update | ComponentDescription | descriptionInfo: DescriptionInfo;                                                                                                                                                                                                                                                                                    | 新增 |
| ohos.update | ComponentDescription | componentId: string;                                                                                                                                                                                                                                                                                                 | 新增 |
| ohos.update | DescriptionOptions   | language: string;                                                                                                                                                                                                                                                                                                    | 新增 |
| ohos.update | DescriptionOptions   | format: DescriptionFormat;                                                                                                                                                                                                                                                                                           | 新增 |
| ohos.update | VersionComponent     | componentId: string;                                                                                                                                                                                                                                                                                                 | 新增 |
| ohos.update | Updater              | getCurrentVersionDescription(descriptionOptions: DescriptionOptions, callback: AsyncCallback<Array\<ComponentDescription>>): void;<br>getCurrentVersionDescription(descriptionOptions: DescriptionOptions): Promise<Array\<ComponentDescription>>;                                                                   | 新增 |
| ohos.update | Updater              | getNewVersionDescription(versionDigestInfo: VersionDigestInfo, descriptionOptions: DescriptionOptions, callback: AsyncCallback<Array\<ComponentDescription>>): void;<br>getNewVersionDescription(versionDigestInfo: VersionDigestInfo, descriptionOptions: DescriptionOptions): Promise<Array\<ComponentDescription>>; | 新增 |
| ohos.update | BusinessSubType | PARAM = 2 | 删除 |