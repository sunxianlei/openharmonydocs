# @ohos.app.ability.errorManager (ErrorManager)

The **ErrorManager** module provides APIs for registering and deregistering error observers. For example, you can use the APIs to register an observer when your application wants to capture JS crashes.

> **NOTE**
> 
> The initial APIs of this module are supported since API version 9. Newly added APIs will be marked with a superscript to indicate their earliest API version.

## Modules to Import
```ts
import errorManager from '@ohos.app.ability.errorManager';
```

## ErrorManager.on

on(type: 'error', observer: ErrorObserver): number;

Registers an error observer.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**Parameters**
 
| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| type | string | Yes| Type of the API to call. It is fixed at **"error"**.|
| observer | [ErrorObserver](./js-apis-inner-application-errorObserver.md) | Yes| Digital code of the observer.|

**Return value**

  | Type| Description|
  | -------- | -------- |
  | number | Index of the observer.|

**Example**
    
```ts
let observer = {
    onUnhandledException(errorMsg) {
        console.log('onUnhandledException, errorMsg: ', errorMsg);
    }
};
let observerId = -1;
try {
    observerId = errorManager.on('error', observer);
} catch (paramError) {
    console.error('error: ${paramError.code}, ${paramError.message}');
}
```

## ErrorManager.off

off(type: 'error', observerId: number,  callback: AsyncCallback\<void>): void;

Deregisters an error observer. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**Parameters**
 
| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| type | string | Yes| Type of the API to call. It is fixed at **"error"**.|
| observerId | number | Yes| Index of the observer returned by **on()**.|
| callback | AsyncCallback\<void> | Yes| Callback used to return the result.|

**Example**
    
```ts
let observerId = 100;

function unregisterErrorObserverCallback(err) {
    if (err) {
        console.error('------------ unregisterErrorObserverCallback ------------', err);
    }
}
try {
    errorManager.off('error', observerId, unregisterErrorObserverCallback);
} catch (paramError) {
    console.error('error: ${paramError.code}, ${paramError.message}');
}
```

## ErrorManager.off

off(type: 'error', observerId: number): Promise\<void>;

Deregisters an error observer. This API uses a promise to return the result.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**Parameters**
 
| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| type | string | Yes| Type of the API to call. It is fixed at **"error"**.|
| observerId | number | Yes| Index of the observer returned by **on()**.|

**Return value**

| Type| Description|
| -------- | -------- |
| Promise\<void> | Promise used to return the result.|

**Example**
    
```ts
let observerId = 100;
try {
    errorManager.off('error', observerId)
        .then((data) => {
            console.log('----------- unregisterErrorObserver success ----------', data);
        })
        .catch((err) => {
            console.error('----------- unregisterErrorObserver fail ----------', err);
    });
} catch (paramError) {
    console.error('error: ${paramError.code}, ${paramError.message}');
}

```
