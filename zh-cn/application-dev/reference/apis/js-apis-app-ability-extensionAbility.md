# ExtensionAbility

ExtensionAbility模块提供对ExtensionAbility生命周期、上下文环境等调用管理的能力，包括ExtensionAbility创建、销毁、转储客户端信息等。

> **说明：**
> 
> 本模块首批接口从API version 9 开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。  
> 本模块接口仅可在Stage模型下使用。

## 导入模块

```ts
import ExtensionAbility from '@ohos.app.ability.ExtensionAbility';
```

**系统能力**：SystemCapability.Ability.AbilityRuntime.AbilityCore

**示例：**
    
  ```ts
  class MyExtensionAbility extends ExtensionAbility {
      onConfigurationUpdated(config) {
          console.log('onConfigurationUpdated, config:' + JSON.stringify(config));
      }

      onMemoryLevel(level) {
          console.log('onMemoryLevel, level:' + JSON.stringify(level));
      }
  }
  ```