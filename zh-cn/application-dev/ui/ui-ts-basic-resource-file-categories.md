# 资源文件的分类

应用开发中使用的各类资源文件，需要放入特定子目录中存储管理。

## resources目录

应用的资源文件（字符串、图片、音频等）统一存放于resources目录下，便于开发者使用和维护。resources目录包括两大类目录，一类为base目录与限定词目录，另一类为rawfile目录，详见resources目录分类。

  资源目录示例：

```
resources
|---base  // 默认存在的目录
|   |---element
|   |   |---string.json
|   |---media
|   |   |---icon.png
|---en_GB-vertical-car-mdpi // 限定词目录示例，需要开发者自行创建   
|   |---element
|   |   |---string.json
|   |---media
|   |   |---icon.png
|---rawfile
```

  **表1** resources目录分类

| 分类   | base目录与限定词目录                             | 限定词目录                                    | rawfile目录                                |
| ---- | ---------------------------------------- | ---------------------------------------- | ---------------------------------------- |
| 组织形式 | base目录是默认存在的目录。当应用的resources目录中没有与设备状态匹配的限定词目录时，会自动引用该目录中的资源文件。<br/>base目录的二级子目录为**资源组目录**，用于存放字符串、颜色、布尔值等基础元素，以及媒体、动画、布局等资源文件，具体要求参见[资源组目录](#资源组目录)。 | 限定词目录需要开发者自行创建。目录名称由一个或多个表征应用场景或设备特征的限定词组合而成，具体要求参见[限定词目录](#限定词目录)。<br/>限定词目录的二级子目录为**资源组目录**，用于存放字符串、颜色、布尔值等基础元素，以及媒体、动画、布局等资源文件，具体要求参见[资源组目录](#资源组目录)。 | 支持创建多层子目录，目录名称可以自定义，文件夹内可以自由放置各类资源文件。<br/>rawfile目录的文件不会根据设备状态去匹配不同的资源。 |
| 编译方式 | 目录中的资源文件会被编译成二进制文件，并赋予资源文件ID。            | 目录中的资源文件会被编译成二进制文件，并赋予资源文件ID。            | 目录中的资源文件会被直接打包进应用，不经过编译，也不会被赋予资源文件ID。    |
| 引用方式 | 通过指定资源类型（type）和资源名称（name）来引用。            | 通过指定资源类型（type）和资源名称（name）来引用。            | 通过指定文件路径和文件名来引用。                         |


## 限定词目录

限定词目录可以由一个或多个表征应用场景或设备特征的限定词组合而成，包括移动国家码和移动网络码、语言、文字、国家或地区、横竖屏、设备类型、颜色模式和屏幕密度等维度，限定词之间通过下划线（_）或者中划线（-）连接。开发者在创建限定词目录时，需要掌握限定词目录的命名要求，以及限定词目录与设备状态的匹配规则。

**限定词目录的命名要求**

- 限定词的组合顺序：_移动国家码_移动网络码-语言_文字_国家或地区-横竖屏-设备类型-颜色模式-屏幕密度_。开发者可以根据应用的使用场景和设备特征，选择其中的一类或几类限定词组成目录名称。

- 限定词的连接方式：语言、文字、国家或地区之间采用下划线（_）连接，移动国家码和移动网络码之间也采用下划线（_）连接，除此之外的其他限定词之间均采用中划线（-）连接。例如：**zh_Hant_CN**、**zh_CN-car-ldpi**。

- 限定词的取值范围：每类限定词的取值必须符合限定词取值要求表中的条件，否则，将无法匹配目录中的资源文件。

**表2** 限定词取值要求

| 限定词类型       | 含义与取值说明                                  |
| ----------- | ---------------------------------------- |
| 移动国家码和移动网络码 | 移动国家码（MCC）和移动网络码（MNC）的值取自设备注册的网络。MCC后面可以跟随MNC，使用下划线（_）连接，也可以单独使用。例如：mcc460表示中国，mcc460_mnc00表示中国_中国移动。<br/>详细取值范围，请查阅**ITU-T&nbsp;E.212**（国际电联相关标准）。 |
| 语言          | 表示设备使用的语言类型，由2~3个小写字母组成。例如：zh表示中文，en表示英语，mai表示迈蒂利语。<br/>详细取值范围，请查阅**ISO&nbsp;639**（ISO制定的语言编码标准）。 |
| 文字          | 表示设备使用的文字类型，由1个大写字母（首字母）和3个小写字母组成。例如：Hans表示简体中文，Hant表示繁体中文。<br/>详细取值范围，请查阅**ISO&nbsp;15924**（ISO制定的文字编码标准）。 |
| 国家或地区       | 表示用户所在的国家或地区，由2~3个大写字母或者3个数字组成。例如：CN表示中国，GB表示英国。<br/>详细取值范围，请查阅**ISO&nbsp;3166-1**（ISO制定的国家和地区编码标准）。 |
| 横竖屏         | 表示设备的屏幕方向，取值如下：<br/>-&nbsp;vertical：竖屏<br/>-&nbsp;horizontal：横屏 |
| 设备类型        | 表示设备的类型，取值如下：<br/>-&nbsp;car：车机<br/>-&nbsp;tv：智慧屏<br/>-&nbsp;wearable：智能穿戴 |
| 颜色模式        | 表示设备的颜色模式，取值如下：<br/>-&nbsp;dark：深色模式<br/>-&nbsp;light：浅色模式 |
| 屏幕密度        | 表示设备的屏幕密度（单位为dpi），取值如下：<br/>-&nbsp;sdpi：表示小规模的屏幕密度（Small-scale&nbsp;Dots&nbsp;Per&nbsp;Inch），适用于dpi取值为(0,&nbsp;120]的设备。<br/>-&nbsp;mdpi：表示中规模的屏幕密度（Medium-scale&nbsp;Dots&nbsp;Per&nbsp;Inch），适用于dpi取值为(120,&nbsp;160]的设备。<br/>-&nbsp;ldpi：表示大规模的屏幕密度（Large-scale&nbsp;Dots&nbsp;Per&nbsp;Inch），适用于dpi取值为(160,&nbsp;240]的设备。<br/>-&nbsp;xldpi：表示特大规模的屏幕密度（Extra&nbsp;Large-scale&nbsp;Dots&nbsp;Per&nbsp;Inch），适用于dpi取值为(240,&nbsp;320]的设备。<br/>-&nbsp;xxldpi：表示超大规模的屏幕密度（Extra&nbsp;Extra&nbsp;Large-scale&nbsp;Dots&nbsp;Per&nbsp;Inch），适用于dpi取值为(320,&nbsp;480]的设备。<br/>-&nbsp;xxxldpi：表示超特大规模的屏幕密度（Extra&nbsp;Extra&nbsp;Extra&nbsp;Large-scale&nbsp;Dots&nbsp;Per&nbsp;Inch），适用于dpi取值为(480,&nbsp;640]的设备。 |

**限定词目录与设备状态的匹配规则**

- 在为设备匹配对应的资源文件时，限定词目录匹配的优先级从高到低依次为：移动国家码和移动网络码 &gt; 区域（可选组合：语言、语言_文字、语言_国家或地区、语言_文字_国家或地区）&gt; 横竖屏 &gt; 设备类型 &gt; 颜色模式 &gt; 屏幕密度。

- 如果限定词目录中包含**移动国家码和移动网络码、语言、文字、横竖屏、设备类型、颜色模式**限定词，则对应限定词的取值必须与当前的设备状态完全一致，该目录才能够参与设备的资源匹配。例如，限定词目录“zh_CN-car-ldpi”不能参与“en_US”设备的资源匹配。


## 资源组目录

base目录与限定词目录下面可以创建资源组目录（包括element、media、animation、layout、graphic、profile），用于存放特定类型的资源文件，详见资源组目录说明。


  **表3** 资源组目录说明

| 资源组目录   | 目录说明                                     | 资源文件                                     |
| ------- | ---------------------------------------- | ---------------------------------------- |
| element | 表示元素资源，以下每一类数据都采用相应的JSON文件来表征。<br/>-&nbsp;boolean，布尔型<br/>-&nbsp;color，颜色<br/>-&nbsp;float，浮点型<br/>-&nbsp;intarray，整型数组<br/>-&nbsp;integer，整型<br/>-&nbsp;pattern，样式<br/>-&nbsp;plural，复数形式<br/>-&nbsp;strarray，字符串数组<br/>-&nbsp;string，字符串 | element目录中的文件名称建议与下面的文件名保持一致。每个文件中只能包含同一类型的数据。<br/>-&nbsp;boolean.json<br/>-&nbsp;color.json<br/>-&nbsp;float.json<br/>-&nbsp;intarray.json<br/>-&nbsp;integer.json<br/>-&nbsp;pattern.json<br/>-&nbsp;plural.json<br/>-&nbsp;strarray.json<br/>-&nbsp;string.json |
| media   | 表示媒体资源，包括图片、音频、视频等非文本格式的文件。              | 文件名可自定义，例如：icon.png。                     |
| rawfile | 表示其他类型文件，在应用构建为hap包后，以原始文件形式保存，不会被集成到resources.index文件中。 | 文件名可自定义。                                 |

### 媒体资源类型说明

表1 图片资源类型说明

| 格式   | 文件后缀名 |
| ---- | ----- |
| JPEG | .jpg  |
| PNG  | .png  |
| GIF  | .gif  |
| SVG  | .svg  |
| WEBP | .webp |
| BMP  | .bmp  |

表2 音视频资源类型说明

| 格式                                   | 支持的文件类型         |
| ------------------------------------ | --------------- |
| H.263                                | .3gp <br>.mp4   |
| H.264 AVC <br> Baseline Profile (BP) | .3gp <br>.mp4   |
| MPEG-4 SP                            | .3gp            |
| VP8                                  | .webm <br> .mkv |

## 创建资源文件

在resources目录下，可按照限定词目录和资源组目录的说明创建子目录和目录内的文件。

同时，DevEco Studio也提供了创建资源目录和资源文件的界面。

- 创建资源目录及资源文件

  在resources目录右键菜单选择“New > Resource File”，此时可同时创建目录和文件。

  文件默认创建在base目录的对应资源组下。如果选择了限定词，则会按照命名规范自动生成限定词+资源组目录，并将文件创建在目录中。

  目录名自动生成，格式固定为“限定词.资源组”，例如创建一个限定词为横竖屏类别下的竖屏，资源组为绘制资源的目录，自动生成的目录名称为“vertical.graphic”。

  ![create-resource-file-1](figures/create-resource-file-1.png)

- 创建资源目录

  在resources目录右键菜单选择“New > Resource Directory”，此时可创建资源目录。

  选择资源组类型，设置限定词，创建后自动生成目录名称。目录名称格式固定为“限定词.资源组”，例如创建一个限定词为横竖屏类别下的竖屏，资源组为绘制资源的目录，自动生成的目录名称为“vertical.graphic”。

  ![create-resource-file-2](figures/create-resource-file-2.png)

- 创建资源文件

  在资源目录的右键菜单选择“New > XXX Resource File”，即可创建对应资源组目录的资源文件。

  例如，在element目录下可新建Element Resource File。

  ![create-resource-file-3](figures/create-resource-file-3.png)