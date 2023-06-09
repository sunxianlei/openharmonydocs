# ServiceExtensionContext

The **ServiceExtensionContext** module, inherited from **ExtensionContext**, provides context for ServiceExtensionAbilities.

You can use the APIs of this module to start, terminate, connect, and disconnect abilities.

> **NOTE**
> 
>  - The initial APIs of this module are supported since API version 9. Newly added APIs will be marked with a superscript to indicate their earliest API version.
>  - The APIs of this module can be used only in the stage model.

## Usage

Before using the **ServiceExtensionContext** module, you must define a child class that inherits from **ServiceExtensionAbility**.

```ts
  import ServiceExtensionAbility from '@ohos.app.ability.ServiceExtensionAbility';

  let context;
  class EntryAbility extends ServiceExtensionAbility {
    onCreate() {
      context = this.context; // Obtain a ServiceExtensionContext instance.
    }
  }
```

## ServiceExtensionContext.startAbility

startAbility(want: Want, callback: AsyncCallback&lt;void&gt;): void;

Starts an ability. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md)  | Yes| Want information about the target ability, such as the ability name and bundle name.|
| callback | AsyncCallback&lt;void&gt; | No| Callback used to return the result.|

**Error codes**

| ID| Error Message|
| ------- | -------------------------------- |
| 201 | The application does not have permission to call the interface. |
| 401 | Invalid input parameter. |
| 16000001 | Input error. The specified ability name does not exist. |
| 16000004 | Visibility verification failed. |
| 16000005 | Static permission denied. The specified process does not have the permission. |
| 16000007 | Service busyness. There are concurrent tasks, waiting for retry. |
| 16000008 | Crowdtest App Expiration. |
| 16000009 | Can not start ability in wukong mode. |
| 16000010 | Can not operation with continue flag.        |
| 16000011 | Context does not exist.        |
| 16000051 | Network error. The network is abnormal. |
| 16000052 | Free install not support. The application does not support freeinstall |
| 16000053 | Not top ability. The application is not top ability. |
| 16000054 | Free install busyness. There are concurrent tasks, waiting for retry. |
| 16000055 | Free install timeout. |
| 16000056 | Can not free install other ability. |
| 16000057 | Not support cross device free install. |
| 16200001 | Caller released. The caller has been released. |
| 16000050 | Internal Error. |

**Example**

  ```ts
  let want = {
    bundleName: 'com.example.myapp',
    abilityName: 'MyAbility'
  };

  try {
    this.context.startAbility(want, (error) => {
      if (error.code) {
        // Process service logic errors.
        console.error('startAbility failed, error.code: ${JSON.stringify(error.code)}, error.message: ${JSON.stringify(error.message)}');
        return;
      }
      // Carry out normal service processing.
      console.log('startAbility succeed');
    });
  } catch (paramError) {
    // Process input parameter errors.
    console.error('error.code: ${JSON.stringify(paramError.code)}, error.message: ${JSON.stringify(paramError.message)}');
  }
  ```

## ServiceExtensionContext.startAbility

startAbility(want: Want, options?: StartOptions): Promise\<void>;

Starts an ability. This API uses a promise to return the result.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md)  | Yes| Want information about the target ability, such as the ability name and bundle name.|
| options | [StartOptions](js-apis-app-ability-startOptions.md) | Yes| Parameters used for starting the ability.|

**Return value**

| Type| Description|
| -------- | -------- |
| Promise&lt;void&gt; | Promise used to return the result.|

**Error codes**

| ID| Error Message|
| ------- | -------------------------------- |
| 201 | The application does not have permission to call the interface. |
| 401 | Invalid input parameter. |
| 16000001 | Input error. The specified ability name does not exist. |
| 16000004 | Visibility verification failed. |
| 16000005 | Static permission denied. The specified process does not have the permission. |
| 16000007 | Service busyness. There are concurrent tasks, waiting for retry. |
| 16000008 | Crowdtest App Expiration. |
| 16000009 | Can not start ability in wukong mode. |
| 16000010 | Can not operation with continue flag.        |
| 16000011 | Context does not exist.        |
| 16000051 | Network error. The network is abnormal. |
| 16000052 | Free install not support. The application does not support freeinstall |
| 16000053 | Not top ability. The application is not top ability. |
| 16000054 | Free install busyness. There are concurrent tasks, waiting for retry. |
| 16000055 | Free install timeout. |
| 16000056 | Can not free install other ability. |
| 16000057 | Not support cross device free install. |
| 16200001 | Caller released. The caller has been released. |
| 16000050 | Internal Error. |

**Example**

  ```ts
  let want = {
    bundleName: 'com.example.myapp',
    abilityName: 'MyAbility'
  };
  let options = {
  	windowMode: 0,
  };

  try {
    this.context.startAbility(want, options)
      .then((data) => {
        // Carry out normal service processing.
        console.log('startAbility succeed');
      })
      .catch((error) => {
        // Process service logic errors.
        console.error('startAbility failed, error.code: ${JSON.stringify(error.code)}, error.message: ${JSON.stringify(error.message)}');
      });
  } catch (paramError) {
    // Process input parameter errors.
    console.error('error.code: ${JSON.stringify(paramError.code)}, error.message: ${JSON.stringify(paramError.message)}');
  }
  ```

## ServiceExtensionContext.startAbility

startAbility(want: Want, options: StartOptions, callback: AsyncCallback&lt;void&gt;): void

Starts an ability. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md)  | Yes| Want information about the target ability.|
| options | [StartOptions](js-apis-app-ability-startOptions.md) | Yes| Parameters used for starting the ability.|
| callback | AsyncCallback&lt;void&gt; | Yes| Callback used to return the result.|

**Error codes**

| ID| Error Message|
| ------- | -------------------------------- |
| 201 | The application does not have permission to call the interface. |
| 401 | Invalid input parameter. |
| 16000001 | Input error. The specified ability name does not exist. |
| 16000004 | Visibility verification failed. |
| 16000005 | Static permission denied. The specified process does not have the permission. |
| 16000007 | Service busyness. There are concurrent tasks, waiting for retry. |
| 16000008 | Crowdtest App Expiration. |
| 16000009 | Can not start ability in wukong mode. |
| 16000010 | Can not operation with continue flag.        |
| 16000011 | Context does not exist.        |
| 16000051 | Network error. The network is abnormal. |
| 16000052 | Free install not support. The application does not support freeinstall |
| 16000053 | Not top ability. The application is not top ability. |
| 16000054 | Free install busyness. There are concurrent tasks, waiting for retry. |
| 16000055 | Free install timeout. |
| 16000056 | Can not free install other ability. |
| 16000057 | Not support cross device free install. |
| 16200001 | Caller released. The caller has been released. |
| 16000050 | Internal Error. |

**Example**

  ```ts
  let want = {
    deviceId: '',
    bundleName: 'com.example.myapplication',
    abilityName: 'EntryAbility'
  };
  let options = {
    windowMode: 0
  };

  try {
    this.context.startAbility(want, options, (error) => {
      if (error.code) {
        // Process service logic errors.
        console.error('startAbility failed, error.code: ${JSON.stringify(error.code)}, error.message: ${JSON.stringify(error.message)}');
        return;
      }
      // Carry out normal service processing.
      console.log('startAbility succeed');
    });
  } catch (paramError) {
    // Process input parameter errors.
    console.error('error.code: ${JSON.stringify(paramError.code)}, error.message: ${JSON.stringify(paramError.message)}');
  }
  ```

## ServiceExtensionContext.startAbilityWithAccount

startAbilityWithAccount(want: Want, accountId: number, callback: AsyncCallback\<void>): void;

Starts an ability with the account ID specified. This API uses an asynchronous callback to return the result.

Observe the following when using this API:
 - If an application running in the background needs to call this API to start an ability, it must have the **ohos.permission.START_ABILITIES_FROM_BACKGROUND** permission.
 - If **visible** of the target ability is **false** in cross-application scenarios, the caller must have the **ohos.permission.START_INVISIBLE_ABILITY** permission.
 - For details about the startup rules for the components in the stage model, see [Component Startup Rules (Stage Model)](../../application-models/component-startup-rules.md).

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | Yes| Want information about the target ability.|
| accountId | number | Yes| ID of a system account. For details, see [getCreatedOsAccountsCount](js-apis-osAccount.md#getosaccountlocalidfromprocess).|
| callback | AsyncCallback\<void\> | Yes| Callback used to return the result.|

**Error codes**

| ID| Error Message|
| ------- | -------------------------------- |
| 201 | The application does not have permission to call the interface. |
| 401 | Invalid input parameter. |
| 16000001 | Input error. The specified ability name does not exist. |
| 16000004 | Visibility verification failed. |
| 16000005 | Static permission denied. The specified process does not have the permission. |
| 16000006 | Can not cross user operations. |
| 16000007 | Service busyness. There are concurrent tasks, waiting for retry. |
| 16000008 | Crowdtest App Expiration. |
| 16000009 | Can not start ability in wukong mode. |
| 16000010 | Can not operation with continue flag.        |
| 16000011 | Context does not exist.        |
| 16000051 | Network error. The network is abnormal. |
| 16000052 | Free install not support. The application does not support freeinstall |
| 16000053 | Not top ability. The application is not top ability. |
| 16000054 | Free install busyness. There are concurrent tasks, waiting for retry. |
| 16000055 | Free install timeout. |
| 16000056 | Can not free install other ability. |
| 16000057 | Not support cross device free install. |
| 16200001 | Caller released. The caller has been released. |
| 16000050 | Internal Error. |

**Example**

  ```ts
  let want = {
    deviceId: '',
    bundleName: 'com.example.myapplication',
    abilityName: 'EntryAbility'
  };
  let accountId = 100;

  try {
    this.context.startAbilityWithAccount(want, accountId, (error) => {
      if (error.code) {
        // Process service logic errors.
        console.error('startAbilityWithAccount failed, error.code: ${JSON.stringify(error.code)}, error.message: ${JSON.stringify(error.message)}');
        return;
      }
      // Carry out normal service processing.
      console.log('startAbilityWithAccount succeed');
    });
  } catch (paramError) {
    // Process input parameter errors.
    console.error('error.code: ${JSON.stringify(paramError.code)}, error.message: ${JSON.stringify(paramError.message)}');
  }
  ```

## ServiceExtensionContext.startAbilityWithAccount

startAbilityWithAccount(want: Want, accountId: number, options: StartOptions, callback: AsyncCallback\<void\>): void;

Starts an ability with the account ID and start options specified. This API uses an asynchronous callback to return the result.

Observe the following when using this API:
 - If an application running in the background needs to call this API to start an ability, it must have the **ohos.permission.START_ABILITIES_FROM_BACKGROUND** permission.
 - If **visible** of the target ability is **false** in cross-application scenarios, the caller must have the **ohos.permission.START_INVISIBLE_ABILITY** permission.
 - For details about the startup rules for the components in the stage model, see [Component Startup Rules (Stage Model)](../../application-models/component-startup-rules.md).

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | Yes| Want information about the target ability.|
| accountId | number | Yes| ID of a system account. For details, see [getCreatedOsAccountsCount](js-apis-osAccount.md#getosaccountlocalidfromprocess).|
| options | [StartOptions](js-apis-app-ability-startOptions.md) | No| Parameters used for starting the ability.|
| callback | AsyncCallback\<void\> | Yes| Callback used to return the result.|

**Error codes**

| ID| Error Message|
| ------- | -------------------------------- |
| 201 | The application does not have permission to call the interface. |
| 401 | Invalid input parameter. |
| 16000001 | Input error. The specified ability name does not exist. |
| 16000004 | Visibility verification failed. |
| 16000005 | Static permission denied. The specified process does not have the permission. |
| 16000006 | Can not cross user operations. |
| 16000007 | Service busyness. There are concurrent tasks, waiting for retry. |
| 16000008 | Crowdtest App Expiration. |
| 16000009 | Can not start ability in wukong mode. |
| 16000010 | Can not operation with continue flag.        |
| 16000011 | Context does not exist.        |
| 16000051 | Network error. The network is abnormal. |
| 16000052 | Free install not support. The application does not support freeinstall |
| 16000053 | Not top ability. The application is not top ability. |
| 16000054 | Free install busyness. There are concurrent tasks, waiting for retry. |
| 16000055 | Free install timeout. |
| 16000056 | Can not free install other ability. |
| 16000057 | Not support cross device free install. |
| 16200001 | Caller released. The caller has been released. |
| 16000050 | Internal Error. |

**Example**

  ```ts
  let want = {
    deviceId: '',
    bundleName: 'com.example.myapplication',
    abilityName: 'EntryAbility'
  };
  let accountId = 100;
  let options = {
    windowMode: 0
  };

  try {
    this.context.startAbilityWithAccount(want, accountId, options, (error) => {
      if (error.code) {
        // Process service logic errors.
        console.error('startAbilityWithAccount failed, error.code: ${JSON.stringify(error.code)}, error.message: ${JSON.stringify(error.message)}');
        return;
      }
      // Carry out normal service processing.
      console.log('startAbilityWithAccount succeed');
    });
  } catch (paramError) {
    // Process input parameter errors.
    console.error('error.code: ${JSON.stringify(paramError.code)}, error.message: ${JSON.stringify(paramError.message)}');
  }
  ```


## ServiceExtensionContext.startAbilityWithAccount

startAbilityWithAccount(want: Want, accountId: number, options?: StartOptions): Promise\<void>;

Starts an ability with the account ID specified. This API uses a promise to return the result.

Observe the following when using this API:
 - If an application running in the background needs to call this API to start an ability, it must have the **ohos.permission.START_ABILITIES_FROM_BACKGROUND** permission.
 - If **visible** of the target ability is **false** in cross-application scenarios, the caller must have the **ohos.permission.START_INVISIBLE_ABILITY** permission.
 - For details about the startup rules for the components in the stage model, see [Component Startup Rules (Stage Model)](../../application-models/component-startup-rules.md).

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | Yes| Want information about the target ability.|
| accountId | number | Yes| ID of a system account. For details, see [getCreatedOsAccountsCount](js-apis-osAccount.md#getosaccountlocalidfromprocess).|
| options | [StartOptions](js-apis-app-ability-startOptions.md) | No| Parameters used for starting the ability.|

**Return value**

| Type| Description|
| -------- | -------- |
| Promise&lt;void&gt; | Promise used to return the result.|

**Error codes**

| ID| Error Message|
| ------- | -------------------------------- |
| 201 | The application does not have permission to call the interface. |
| 401 | Invalid input parameter. |
| 16000001 | Input error. The specified ability name does not exist. |
| 16000004 | Visibility verification failed. |
| 16000005 | Static permission denied. The specified process does not have the permission. |
| 16000006 | Can not cross user operations. |
| 16000007 | Service busyness. There are concurrent tasks, waiting for retry. |
| 16000008 | Crowdtest App Expiration. |
| 16000009 | Can not start ability in wukong mode. |
| 16000010 | Can not operation with continue flag.        |
| 16000011 | Context does not exist.        |
| 16000051 | Network error. The network is abnormal. |
| 16000052 | Free install not support. The application does not support freeinstall |
| 16000053 | Not top ability. The application is not top ability. |
| 16000054 | Free install busyness. There are concurrent tasks, waiting for retry. |
| 16000055 | Free install timeout. |
| 16000056 | Can not free install other ability. |
| 16000057 | Not support cross device free install. |
| 16200001 | Caller released. The caller has been released. |
| 16000050 | Internal Error. |

**Example**

  ```ts
  let want = {
    deviceId: '',
    bundleName: 'com.example.myapplication',
    abilityName: 'EntryAbility'
  };
  let accountId = 100;
  let options = {
    windowMode: 0
  };

  try {
    this.context.startAbilityWithAccount(want, accountId, options)
      .then((data) => {
        // Carry out normal service processing.
        console.log('startAbilityWithAccount succeed');
      })
      .catch((error) => {
        // Process service logic errors.
        console.error('startAbilityWithAccount failed, error.code: ${JSON.stringify(error.code)}, error.message: ${JSON.stringify(error.message)}');
      });
  } catch (paramError) {
    // Process input parameter errors.
    console.error('error.code: ${JSON.stringify(paramError.code)}, error.message: ${JSON.stringify(paramError.message)}');
  }
  ```

## ServiceExtensionContext.startServiceExtensionAbility

startServiceExtensionAbility(want: Want, callback: AsyncCallback\<void>): void;

Starts a new ServiceExtensionAbility. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | Yes| Want information about the target ability.|
| callback | AsyncCallback\<void\> | Yes| Callback used to return the result.|

**Error codes**

| ID| Error Message|
| ------- | -------------------------------- |
| 201 | The application does not have permission to call the interface. |
| 401 | Invalid input parameter. |
| 16000001 | Input error. The specified ability name does not exist. |
| 16000002 | Ability type error. The specified ability type is wrong. |
| 16000004 | Visibility verification failed. |
| 16000005 | Static permission denied. The specified process does not have the permission. |
| 16000007 | Service busyness. There are concurrent tasks, waiting for retry. |
| 16000008 | Crowdtest App Expiration. |
| 16000009 | Can not start ability in wukong mode. |
| 16000011 | Context does not exist.        |
| 16200001 | Caller released. The caller has been released. |
| 16000050 | Internal Error. |

**Example**

  ```ts
  let want = {
    deviceId: '',
    bundleName: 'com.example.myapplication',
    abilityName: 'EntryAbility'
  };

  try {
    this.context.startServiceExtensionAbility(want, (error) => {
      if (error.code) {
        // Process service logic errors.
        console.error('startServiceExtensionAbility failed, error.code: ${JSON.stringify(error.code)}, error.message: ${JSON.stringify(error.message)}');
        return;
      }
      // Carry out normal service processing.
      console.log('startServiceExtensionAbility succeed');
    });
  } catch (paramError) {
    // Process input parameter errors.
    console.error('error.code: ${JSON.stringify(paramError.code)}, error.message: ${JSON.stringify(paramError.message)}');
  }
  ```

## ServiceExtensionContext.startServiceExtensionAbility

startServiceExtensionAbility(want: Want): Promise\<void>;

Starts a new ServiceExtensionAbility. This API uses a promise to return the result.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | Yes| Want information about the target ability.|

**Return value**

| Type| Description|
| -------- | -------- |
| Promise&lt;void&gt; | Promise used to return the result.|

**Error codes**

| ID| Error Message|
| ------- | -------------------------------- |
| 201 | The application does not have permission to call the interface. |
| 401 | Invalid input parameter. |
| 16000001 | Input error. The specified ability name does not exist. |
| 16000002 | Ability type error. The specified ability type is wrong. |
| 16000004 | Visibility verification failed. |
| 16000005 | Static permission denied. The specified process does not have the permission. |
| 16000007 | Service busyness. There are concurrent tasks, waiting for retry. |
| 16000008 | Crowdtest App Expiration. |
| 16000009 | Can not start ability in wukong mode. |
| 16000011 | Context does not exist.        |
| 16200001 | Caller released. The caller has been released. |
| 16000050 | Internal Error. |

**Example**

  ```ts
  let want = {
    deviceId: '',
    bundleName: 'com.example.myapplication',
    abilityName: 'EntryAbility'
  };

  try {
    this.context.startServiceExtensionAbility(want)
      .then((data) => {
        // Carry out normal service processing.
        console.log('startServiceExtensionAbility succeed');
      })
      .catch((error) => {
        // Process service logic errors.
        console.error('startServiceExtensionAbility failed, error.code: ${JSON.stringify(error.code)}, error.message: ${JSON.stringify(error.message)}');
      });
  } catch (paramError) {
    // Process input parameter errors.
    console.error('error.code: ${JSON.stringify(paramError.code)}, error.message: ${JSON.stringify(paramError.message)}');
  }
  ```

## ServiceExtensionContext.startServiceExtensionAbilityWithAccount

startServiceExtensionAbilityWithAccount(want: Want, accountId: number, callback: AsyncCallback\<void>): void;

Starts a new ServiceExtensionAbility with the account ID specified. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.INTERACT_ACROSS_LOCAL_ACCOUNTS (required only when the account ID is not the current user)

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | Yes| Want information about the target ability.|
| accountId | number | Yes| ID of a system account. For details, see [getCreatedOsAccountsCount](js-apis-osAccount.md#getosaccountlocalidfromprocess).|
| callback | AsyncCallback\<void\> | Yes| Callback used to return the result.|

**Error codes**

| ID| Error Message|
| ------- | -------------------------------- |
| 201 | The application does not have permission to call the interface. |
| 401 | Invalid input parameter. |
| 16000001 | Input error. The specified ability name does not exist. |
| 16000002 | Ability type error. The specified ability type is wrong. |
| 16000004 | Visibility verification failed. |
| 16000005 | Static permission denied. The specified process does not have the permission. |
| 16000006 | Can not cross user operations. |
| 16000007 | Service busyness. There are concurrent tasks, waiting for retry. |
| 16000008 | Crowdtest App Expiration. |
| 16000009 | Can not start ability in wukong mode. |
| 16000011 | Context does not exist.        |
| 16200001 | Caller released. The caller has been released. |
| 16000050 | Internal Error. |


**Example**

  ```ts
  let want = {
    deviceId: '',
    bundleName: 'com.example.myapplication',
    abilityName: 'EntryAbility'
  };
  let accountId = 100;

  try {
    this.context.startServiceExtensionAbilityWithAccount(want, accountId, (error) => {
      if (error.code) {
        // Process service logic errors.
        console.error('startServiceExtensionAbilityWithAccount failed, error.code: ${JSON.stringify(error.code)}, error.message: ${JSON.stringify(error.message)}');
        return;
      }
      // Carry out normal service processing.
      console.log('startServiceExtensionAbilityWithAccount succeed');
    });
  } catch (paramError) {
    // Process input parameter errors.
    console.error('error.code: ${JSON.stringify(paramError.code)}, error.message: ${JSON.stringify(paramError.message)}');
  }
  ```

## ServiceExtensionContext.startServiceExtensionAbilityWithAccount

startServiceExtensionAbilityWithAccount(want: Want, accountId: number): Promise\<void>;

Starts a new ServiceExtensionAbility with the account ID specified. This API uses a promise to return the result.

**Required permissions**: ohos.permission.INTERACT_ACROSS_LOCAL_ACCOUNTS (required only when the account ID is not the current user)

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | Yes| Want information about the target ability.|
| accountId | number | Yes| ID of a system account. For details, see [getCreatedOsAccountsCount](js-apis-osAccount.md#getosaccountlocalidfromprocess).|

**Return value**

| Type| Description|
| -------- | -------- |
| Promise&lt;void&gt; | Promise used to return the result.|

**Error codes**

| ID| Error Message|
| ------- | -------------------------------- |
| 201 | The application does not have permission to call the interface. |
| 401 | Invalid input parameter. |
| 16000001 | Input error. The specified ability name does not exist. |
| 16000002 | Ability type error. The specified ability type is wrong. |
| 16000004 | Visibility verification failed. |
| 16000005 | Static permission denied. The specified process does not have the permission. |
| 16000006 | Can not cross user operations. |
| 16000007 | Service busyness. There are concurrent tasks, waiting for retry. |
| 16000008 | Crowdtest App Expiration. |
| 16000009 | Can not start ability in wukong mode. |
| 16000011 | Context does not exist.        |
| 16200001 | Caller released. The caller has been released. |
| 16000050 | Internal Error. |

**Example**

  ```ts
  let want = {
    deviceId: '',
    bundleName: 'com.example.myapplication',
    abilityName: 'EntryAbility'
  };
  let accountId = 100;

  try {
    this.context.startServiceExtensionAbilityWithAccount(want, accountId)
      .then((data) => {
        // Carry out normal service processing.
        console.log('startServiceExtensionAbilityWithAccount succeed');
      })
      .catch((error) => {
        // Process service logic errors.
        console.error('startServiceExtensionAbilityWithAccount failed, error.code: ${JSON.stringify(error.code)}, error.message: ${JSON.stringify(error.message)}');
      });
  } catch (paramError) {
    // Process input parameter errors.
    console.error('error.code: ${JSON.stringify(paramError.code)}, error.message: ${JSON.stringify(paramError.message)}');
  }
  ```

## ServiceExtensionContext.stopServiceExtensionAbility

stopServiceExtensionAbility(want: Want, callback: AsyncCallback\<void>): void;

Stops a ServiceExtensionAbility in the same application. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | Yes| Want information about the target ability.|
| callback | AsyncCallback\<void\> | Yes| Callback used to return the result.|

**Error codes**

| ID| Error Message|
| ------- | -------------------------------- |
| 201 | The application does not have permission to call the interface. |
| 401 | Invalid input parameter. |
| 16000001 | Input error. The specified ability name does not exist. |
| 16000002 | Ability type error. The specified ability type is wrong. |
| 16000004 | Visibility verification failed. |
| 16000007 | Service busyness. There are concurrent tasks, waiting for retry. |
| 16000011 | Context does not exist.        |
| 16200001 | Caller released. The caller has been released. |
| 16000050 | Internal Error. |

**Example**

  ```ts
  let want = {
    deviceId: '',
    bundleName: 'com.example.myapplication',
    abilityName: 'EntryAbility'
  };

  try {
    this.context.stopServiceExtensionAbility(want, (error) => {
      if (error.code) {
        // Process service logic errors.
        console.error('stopServiceExtensionAbility failed, error.code: ${JSON.stringify(error.code)}, error.message: ${JSON.stringify(error.message)}');
        return;
      }
      // Carry out normal service processing.
      console.log('stopServiceExtensionAbility succeed');
    });
  } catch (paramError) {
    // Process input parameter errors.
    console.error('error.code: ${JSON.stringify(paramError.code)}, error.message: ${JSON.stringify(paramError.message)}');
  }
  ```

## ServiceExtensionContext.stopServiceExtensionAbility

stopServiceExtensionAbility(want: Want): Promise\<void>;

Stops a ServiceExtensionAbility in the same application. This API uses a promise to return the result.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | Yes| Want information about the target ability.|

**Return value**

| Type| Description|
| -------- | -------- |
| Promise&lt;void&gt; | Promise used to return the result.|

**Error codes**

| ID| Error Message|
| ------- | -------------------------------- |
| 201 | The application does not have permission to call the interface. |
| 401 | Invalid input parameter. |
| 16000001 | Input error. The specified ability name does not exist. |
| 16000002 | Ability type error. The specified ability type is wrong. |
| 16000004 | Visibility verification failed. |
| 16000007 | Service busyness. There are concurrent tasks, waiting for retry. |
| 16000011 | Context does not exist.        |
| 16200001 | Caller released. The caller has been released. |
| 16000050 | Internal Error. |

**Example**

  ```ts
  let want = {
    deviceId: '',
    bundleName: 'com.example.myapplication',
    abilityName: 'EntryAbility'
  };

  try {
    this.context.stopServiceExtensionAbility(want)
      .then((data) => {
        // Carry out normal service processing.
        console.log('stopServiceExtensionAbility succeed');
      })
      .catch((error) => {
        // Process service logic errors.
        console.error('stopServiceExtensionAbility failed, error.code: ${JSON.stringify(error.code)}, error.message: ${JSON.stringify(error.message)}');
      });
  } catch (paramError) {
    // Process input parameter errors.
    console.error('error.code: ${JSON.stringify(paramError.code)}, error.message: ${JSON.stringify(paramError.message)}');
  }
  ```

## ServiceExtensionContext.stopServiceExtensionAbilityWithAccount

stopServiceExtensionAbilityWithAccount(want: Want, accountId: number, callback: AsyncCallback\<void>): void;

Stops a ServiceExtensionAbility in the same application with the account ID specified. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.INTERACT_ACROSS_LOCAL_ACCOUNTS (required only when the account ID is not the current user)

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | Yes| Want information about the target ability.|
| accountId | number | Yes| ID of a system account. For details, see [getCreatedOsAccountsCount](js-apis-osAccount.md#getosaccountlocalidfromprocess).|
| callback | AsyncCallback\<void\> | Yes| Callback used to return the result.|

**Error codes**

| ID| Error Message|
| ------- | -------------------------------- |
| 201 | The application does not have permission to call the interface. |
| 401 | Invalid input parameter. |
| 16000001 | Input error. The specified ability name does not exist. |
| 16000002 | Ability type error. The specified ability type is wrong. |
| 16000004 | Visibility verification failed. |
| 16000006 | Can not cross user operations. |
| 16000007 | Service busyness. There are concurrent tasks, waiting for retry. |
| 16000011 | Context does not exist.        |
| 16200001 | Caller released. The caller has been released. |
| 16000050 | Internal Error. |

**Example**

  ```ts
  let want = {
    deviceId: '',
    bundleName: 'com.example.myapplication',
    abilityName: 'EntryAbility'
  };
  let accountId = 100;

  try {
    this.context.stopServiceExtensionAbilityWithAccount(want, accountId, (error) => {
      if (error.code) {
        // Process service logic errors.
        console.error('stopServiceExtensionAbilityWithAccount failed, error.code: ${JSON.stringify(error.code), error.message: ${JSON.stringify(error.message)}');
        return;
      }
      // Carry out normal service processing.
      console.log('stopServiceExtensionAbilityWithAccount succeed');
    });
  } catch (paramError) {
    // Process input parameter errors.
    console.error('error.code: ${JSON.stringify(paramError.code)}, error.message: ${JSON.stringify(paramError.message)}');
  }
  ```

## ServiceExtensionContext.stopServiceExtensionAbilityWithAccount

stopServiceExtensionAbilityWithAccount(want: Want, accountId: number): Promise\<void>;

Stops a ServiceExtensionAbility in the same application with the account ID specified. This API uses a promise to return the result.

**Required permissions**: ohos.permission.INTERACT_ACROSS_LOCAL_ACCOUNTS (required only when the account ID is not the current user)

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | Yes| Want information about the target ability.|
| accountId | number | Yes| ID of a system account. For details, see [getCreatedOsAccountsCount](js-apis-osAccount.md#getosaccountlocalidfromprocess).|

**Return value**

| Type| Description|
| -------- | -------- |
| Promise&lt;void&gt; | Promise used to return the result.|

**Error codes**

| ID| Error Message|
| ------- | -------------------------------- |
| 201 | The application does not have permission to call the interface. |
| 401 | Invalid input parameter. |
| 16000001 | Input error. The specified ability name does not exist. |
| 16000002 | Ability type error. The specified ability type is wrong. |
| 16000004 | Visibility verification failed. |
| 16000006 | Can not cross user operations. |
| 16000007 | Service busyness. There are concurrent tasks, waiting for retry. |
| 16000011 | Context does not exist.        |
| 16200001 | Caller released. The caller has been released. |
| 16000050 | Internal Error. |

**Example**

  ```ts
  let want = {
    deviceId: '',
    bundleName: 'com.example.myapplication',
    abilityName: 'EntryAbility'
  };
  let accountId = 100;

  try {
    this.context.stopServiceExtensionAbilityWithAccount(want, accountId)
      .then((data) => {
        // Carry out normal service processing.
        console.log('stopServiceExtensionAbilityWithAccount succeed');
      })
      .catch((error) => {
        // Process service logic errors.
        console.error('stopServiceExtensionAbilityWithAccount failed, error.code: ${JSON.stringify(error.code)}, error.message: ${JSON.stringify(error.message)}');
      });
  } catch (paramError) {
    // Process input parameter errors.
    console.error('error.code: ${JSON.stringify(paramError.code)}, error.message: ${JSON.stringify(paramError.message)}');
  }
  ```

## ServiceExtensionContext.terminateSelf

terminateSelf(callback: AsyncCallback&lt;void&gt;): void;

Terminates this ability. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| callback | AsyncCallback&lt;void&gt; | No| Callback used to return the result.|

**Error codes**

| ID| Error Message|
| ------- | -------------------------------- |
| 201 | The application does not have permission to call the interface. |
| 401 | Invalid input parameter. |
| 16000001 | Input error. The specified ability name does not exist. |
| 16000007 | Service busyness. There are concurrent tasks, waiting for retry. |
| 16000011 | Context does not exist.        |
| 16000050 | Internal Error. |

**Example**

  ```ts
  this.context.terminateSelf((error) => {
    if (error.code) {
      // Process service logic errors.
      console.error('terminateSelf failed, error.code: ${JSON.stringify(error.code)}, error.message: ${JSON.stringify(error.message)}');
      return;
    }
    // Carry out normal service processing.
    console.log('terminateSelf succeed');
  });
  ```

## ServiceExtensionContext.terminateSelf

terminateSelf(): Promise&lt;void&gt;;

Terminates this ability. This API uses a promise to return the result.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Return value**

| Type| Description|
| -------- | -------- |
| Promise&lt;void&gt; | Promise used to return the result.|

**Error codes**

| ID| Error Message|
| ------- | -------------------------------- |
| 201 | The application does not have permission to call the interface. |
| 401 | Invalid input parameter. |
| 16000001 | Input error. The specified ability name does not exist. |
| 16000007 | Service busyness. There are concurrent tasks, waiting for retry. |
| 16000011 | Context does not exist.        |
| 16000050 | Internal Error. |

**Example**

  ```ts
  this.context.terminateSelf().then((data) => {
    // Carry out normal service processing.
    console.log('terminateSelf succeed');
  }).catch((error) => {
    // Process service logic errors.
    console.error('terminateSelf failed, error.code: ${JSON.stringify(error.code)}, error.message: ${JSON.stringify(error.message)}');
  });
  ```

## ServiceExtensionContext.connectServiceExtensionAbility

connectServiceExtensionAbility(want: Want, options: ConnectOptions): number;

Connects this ability to a ServiceAbility.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md)  | Yes| Want information about the target ability, such as the ability name and bundle name.|
| options | [ConnectOptions](js-apis-inner-ability-connectOptions.md) | Yes| Callback used to return the information indicating that the connection is successful, interrupted, or failed.|

**Return value**

| Type| Description|
| -------- | -------- |
| number | A number, based on which the connection will be interrupted.|

**Error codes**

| ID| Error Message|
| ------- | -------------------------------- |
| 201 | The application does not have permission to call the interface. |
| 401 | Invalid input parameter. |
| 16000001 | Input error. The specified ability name does not exist. |
| 16000002 | Ability type error. The specified ability type is wrong. |
| 16000004 | Visibility verification failed. |
| 16000011 | Context does not exist.        |
| 16000050 | Internal Error. |

**Example**

  ```ts
  let want = {
    bundleName: 'com.example.myapp',
    abilityName: 'MyAbility'
  };
  let options = {
    onConnect(elementName, remote) { console.log('----------- onConnect -----------') },
    onDisconnect(elementName) { console.log('----------- onDisconnect -----------') },
    onFailed(code) { console.error('----------- onFailed -----------') }
  };

  let connection = null;
  try {
    connection = this.context.connectServiceExtensionAbility(want, options);
  } catch (paramError) {
    // Process input parameter errors.
    console.error('error.code: ${JSON.stringify(paramError.code)}, error.message: ${JSON.stringify(paramError.message)}');
  }
  ```

## ServiceExtensionContext.connectServiceExtensionAbilityWithAccount

connectServiceExtensionAbilityWithAccount(want: Want, accountId: number, options: ConnectOptions): number;

Uses the **AbilityInfo.AbilityType.SERVICE** template and account ID to connect this ability to another ability.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | Yes| Want information about the target ability.|
| accountId | number | Yes| ID of a system account. For details, see [getCreatedOsAccountsCount](js-apis-osAccount.md#getosaccountlocalidfromprocess).|
| options | ConnectOptions | No| Remote object instance.|

**Return value**

| Type| Description|
| -------- | -------- |
| number | Result code of the ability connection.|

**Error codes**

| ID| Error Message|
| ------- | -------------------------------- |
| 201 | The application does not have permission to call the interface. |
| 401 | Invalid input parameter. |
| 16000001 | Input error. The specified ability name does not exist. |
| 16000002 | Ability type error. The specified ability type is wrong. |
| 16000004 | Visibility verification failed. |
| 16000006 | Can not cross user operations. |
| 16000011 | Context does not exist.        |
| 16000050 | Internal Error. |

**Example**

  ```ts
  let want = {
    deviceId: '',
    bundleName: 'com.example.myapplication',
    abilityName: 'EntryAbility'
  };
  let accountId = 100;
  let options = {
    onConnect(elementName, remote) { console.log('----------- onConnect -----------'); },
    onDisconnect(elementName) { console.log('----------- onDisconnect -----------'); },
    onFailed(code) { console.log('----------- onFailed -----------'); }
  };

  let connection = null;
  try {
    connection = this.context.connectServiceExtensionAbilityWithAccount(want, accountId, options);
  } catch (paramError) {
    // Process input parameter errors.
    console.error('error.code: ${JSON.stringify(paramError.code)}, error.message: ${JSON.stringify(paramError.message)}');
  }
  ```

## ServiceExtensionContext.disconnectServiceExtensionAbility

disconnectServiceExtensionAbility(connection: number, callback:AsyncCallback&lt;void&gt;): void;

Disconnects this ability from the ServiceAbility. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| connection | number | Yes| Number returned after **connectServiceExtensionAbility** is called.|
| callback | AsyncCallback&lt;void&gt; | No| Callback used to return the result.|

**Error codes**

| ID| Error Message|
| ------- | -------------------------------- |
| 201 | The application does not have permission to call the interface. |
| 401 | Invalid input parameter. |
| 16000001 | Input error. The specified ability name does not exist. |
| 16000003 | Input error. The specified id does not exist. |
| 16000011 | Context does not exist.        |
| 16000050 | Internal Error. |

**Example**

  ```ts
  // connection is the return value of connectServiceExtensionAbility.
  let connection = 1;

  try {
    this.context.disconnectServiceExtensionAbility(connection, (error) => {
      if (error.code) {
        // Process service logic errors.
        console.error('disconnectServiceExtensionAbility failed, error.code: ${JSON.stringify(error.code)}, error.message: ${JSON.stringify(error.message)}');
        return;
      }
      // Carry out normal service processing.
      console.log('disconnectServiceExtensionAbility succeed');
    });
  } catch (paramError) {
    // Process input parameter errors.
    console.error('error.code: ${JSON.stringify(paramError.code)}, error.message: ${JSON.stringify(paramError.message)}');
  }
  ```

## ServiceExtensionContext.disconnectServiceExtensionAbility

disconnectServiceExtensionAbility(connection: number): Promise&lt;void&gt;;

Disconnects this ability from the ServiceAbility. This API uses a promise to return the result.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| connection | number | Yes| Number returned after **connectServiceExtensionAbility** is called.|

**Return value**

| Type| Description|
| -------- | -------- |
| Promise&lt;void&gt; | Promise used to return the result.|

**Error codes**

| ID| Error Message|
| ------- | -------------------------------- |
| 201 | The application does not have permission to call the interface. |
| 401 | Invalid input parameter. |
| 16000001 | Input error. The specified ability name does not exist. |
| 16000003 | Input error. The specified id does not exist. |
| 16000011 | Context does not exist.        |
| 16000050 | Internal Error. |

**Example**

  ```ts
  // connection is the return value of connectServiceExtensionAbility.
  let connection = 1;

  try {
    this.context.disconnectServiceExtensionAbility(connection)
      .then((data) => {
        // Carry out normal service processing.
        console.log('disconnectServiceExtensionAbility succeed');
      })
      .catch((error) => {
        // Process service logic errors.
        console.error('disconnectServiceExtensionAbility failed, error.code: ${JSON.stringify(error.code)}, error.message: ${JSON.stringify(error.message)}');
      });
  } catch (paramError) {
    // Process input parameter errors.
    console.error('error.code: ${JSON.stringify(paramError.code)}, error.message: ${JSON.stringify(paramError.message)}');
  }
  ```

## ServiceExtensionContext.startAbilityByCall

startAbilityByCall(want: Want): Promise&lt;Caller&gt;;

Starts an ability in the foreground or background and obtains the caller object for communicating with the ability.

Observe the following when using this API:
 - If an application running in the background needs to call this API to start an ability, it must have the **ohos.permission.START_ABILITIES_FROM_BACKGROUND** permission.
 - If **visible** of the target ability is **false** in cross-application scenarios, the caller must have the **ohos.permission.START_INVISIBLE_ABILITY** permission.
 - The rules for using this API in the same-device and cross-device scenarios are different. For details, see [Component Startup Rules (Stage Model)](../../application-models/component-startup-rules.md).

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | Yes| Information about the ability to start, including **abilityName**, **moduleName**, **bundleName**, **deviceId** (optional), and **parameters** (optional). If **deviceId** is left blank or null, the local ability is started. If **parameters** is left blank or null, the ability is started in the background.|

**Return value**

| Type| Description|
| -------- | -------- |
| Promise&lt;Caller&gt; | Promise used to return the caller object to communicate with.|

**Error codes**

| ID| Error Message|
| ------- | -------------------------------- |
| 201 | The application does not have permission to call the interface. |
| 401 | Invalid input parameter. |
| 16000001 | Input error. The specified ability name does not exist. |
| 16000004 | Visibility verification failed. |
| 16000005 | Static permission denied. The specified process does not have the permission. |
| 16000007 | Service busyness. There are concurrent tasks, waiting for retry. |
| 16000008 | Crowdtest App Expiration. |
| 16000009 | Can not start ability in wukong mode. |
| 16000050 | Internal Error. |

**Example**

  Start an ability in the background.

  ```ts
  let caller;

  // Start an ability in the background by not passing parameters.
  let wantBackground = {
      bundleName: 'com.example.myservice',
      moduleName: 'entry',
      abilityName: 'EntryAbility',
      deviceId: ''
  };

  try {
    this.context.startAbilityByCall(wantBackground)
      .then((obj) => {
        // Carry out normal service processing.
        caller = obj;
        console.log('startAbilityByCall succeed');
      }).catch((error) => {
        // Process service logic errors.
        console.error('startAbilityByCall failed, error.code: ${JSON.stringify(error.code)}, error.message: ${JSON.stringify(error.message)}');
      });
  } catch (paramError) {
    // Process input parameter errors.
    console.error('error.code: ${JSON.stringify(paramError.code)}, error.message: ${JSON.stringify(paramError.message)}');
  }
  ```

  Start an ability in the foreground.

  ```ts
  let caller;

  // Start an ability in the foreground with 'ohos.aafwk.param.callAbilityToForeground' in parameters set to true.
  let wantForeground = {
      bundleName: 'com.example.myservice',
      moduleName: 'entry',
      abilityName: 'EntryAbility',
      deviceId: '',
      parameters: {
        'ohos.aafwk.param.callAbilityToForeground': true
      }
  };

  try {
    this.context.startAbilityByCall(wantForeground)
      .then((obj) => {
        // Carry out normal service processing.
        caller = obj;
        console.log('startAbilityByCall succeed');
      }).catch((error) => {
        // Process service logic errors.
        console.error('startAbilityByCall failed, error.code: ${JSON.stringify(error.code)}, error.message: ${JSON.stringify(error.message)}');
      });
  } catch (paramError) {
    // Process input parameter errors.
    console.error('error.code: ${JSON.stringify(paramError.code)}, error.message: ${JSON.stringify(paramError.message)}');
  }
  ```
