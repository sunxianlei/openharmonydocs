# @ohos.arkui.drawableDescriptor  (DrawableDescriptor)

本模块提供获取pixelMap的能力，包括前景、背景、蒙版和分层图标。

> **说明：**
>
> 本模块首批接口从API version 10开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。
>
> 示例效果请以真机运行为准，当前IDE预览器不支持。

## 导入模块

```js
import { DrawableDescriptor, LayeredDrawableDescriptor } from '@ohos.arkui.drawableDescriptor';
```

## DrawableDescriptor.constructor
constructor()

创建DrawableDescriptor或LayeredDrawableDescriptor对象。对象构造需要使用全球化接口[getDrawableDescriptor](js-apis-resource-manager.md##getdrawabledescriptor)或[getDrawableDescriptorByName](js-apis-resource-manager.md##getdrawabledescriptorbyname)。

**系统接口：** 此接口为系统接口。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

### DrawableDescriptor

当传入资源id或name为普通图片时，生成DrawableDescriptor对象。

### LayeredDrawableDescriptor

当传入资源id或name为包含前景和背景资源的json文件时，生成LayeredDrawableDescriptor对象。

**示例：**
```js
@Entry
@Component
struct Index {
  private resManager = getContext().resourceManager
  let drawable1 = resManager.getDrawableDescriptor($r('app.media.icon').id)
  let drawable2 = resManager.getDrawableDescriptorByName(icon)
  let layeredDrawable1 = resManager.getDrawableDescriptor($r('app.media.file').id)
  let layeredDrawable1 = resManager.getDrawableDescriptor(file)
 }
```

## DrawableDescriptor.getPixelMap
getPixelMap(): image.PixelMap;

获取pixelMap。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**返回值：**

| 类型                              | 说明              |
| --------------------------------- | ---------------- |
| [image.PixelMap](../apis/js-apis-image.md#pixelmap7) | PixelMap |

**示例：**
  ```js
  @State pixmap: PixelMap = drawable1.getPixelMap();
  ```

## LayeredDrawableDescriptor.getPixelMap
getPixelMap(): image.PixelMap;

获取前景、背景和蒙版融合裁剪后的pixelMap。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**返回值：**

| 类型                              | 说明              |
| --------------------------------- | ---------------- |
| [image.PixelMap](../apis/js-apis-image.md#pixelmap7) | PixelMap |

**示例：**
  ```js
  @State pixmap: PixelMap = layeredDrawable1.getPixelMap();
  ```

## LayeredDrawableDescriptor.getForeground
getForeground(): DrawableDescriptor;

获取前景的DrawableDescriptor对象。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**返回值：**

| 类型                              | 说明              |
| --------------------------------- | ---------------- |
| [DrawableDescriptor](#drawabledescriptor) | DrawableDescriptor对象 |

**示例：**
  ```js
  @State drawable: DrawableDescriptor = layeredDrawable1.getForeground();
  ```

## LayeredDrawableDescriptor.getBackground
getBackground(): DrawableDescriptor;

获取背景的DrawableDescriptor对象。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**返回值：**

| 类型                              | 说明              |
| --------------------------------- | ---------------- |
| [DrawableDescriptor](#drawabledescriptor) | DrawableDescriptor对象 |

**示例：**
  ```js
  @State drawable: DrawableDescriptor = layeredDrawable1.getBackground();
  ```

## LayeredDrawableDescriptor.getMask
getMask(): DrawableDescriptor;

获取蒙版的DrawableDescriptor对象。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**返回值：**

| 类型                              | 说明              |
| --------------------------------- | ---------------- |
| [DrawableDescriptor](#drawabledescriptor) | DrawableDescriptor对象 |

**示例：**
  ```js
  @State drawable: DrawableDescriptor = layeredDrawable1.getMask();
  ```
