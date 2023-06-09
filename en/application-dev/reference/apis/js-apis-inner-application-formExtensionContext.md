# FormExtensionContext

The **FormExtensionContext** module, inherited from **ExtensionContext**, provides context for FormExtensionAbilities.

You can use the APIs of this module to start FormExtensionAbilities.

> **NOTE**
>
> The initial APIs of this module are supported since API version 9. Newly added APIs will be marked with a superscript to indicate their earliest API version.
> The APIs of this module can be used only in the stage model.

## Usage

Before using the **ServiceExtensionContext** module, you must first obtain a **FormExtensionAbility** instance.

```ts
import FormExtensionAbility from '@ohos.app.form.FormExtensionAbility';
import formBindingData from '@ohos.app.form.formBindingData';

export default class MyFormExtensionAbility extends FormExtensionAbility {
  onAddForm(want) {
    let formContext = this.context; // Obtain a FormExtensionContext instance.
    // ...
    let dataObj1 = {
      temperature: '11c',
      'time': '11:00'
    };
    let obj1 = formBindingData.createFormBindingData(dataObj1);
    return obj1;
  }
};
```

## startAbility

startAbility(want: Want, callback: AsyncCallback&lt;void&gt;): void

Starts an ability. This API uses an asynchronous callback to return the result.

**System API**: This is a system API.

**System capability**: SystemCapability.Ability.Form

**Parameters**

| Name|                Type              | Mandatory|              Description              |
| ------| --------------------------------- | ---- | -------------------------------------- |
| want| [Want](js-apis-application-want.md) | Yes | Information about the ability to start, such as the bundle name, ability name, and custom parameters.|
| callback| AsyncCallback&lt;void&gt;       | Yes | Callback used to return the result. If the ability is started, **err** is undefined; otherwise, **err** is an error object.|

**Example**

```ts
import FormExtensionAbility from '@ohos.app.form.FormExtensionAbility';

export default class MyFormExtensionAbility extends FormExtensionAbility {
  onFormEvent(formId, message) {
    // Call startAbility() when the message event is triggered.
    console.log('FormExtensionAbility onFormEvent, formId: ${formId}, message:${message}');
    let want = {
      deviceId: '',
      bundleName: 'com.example.formstartability',
      abilityName: 'EntryAbility',
      parameters: {
        'message': message
      }
    };
    this.context.startAbility(want, (error, data) => {
      if (error) {
        console.error('FormExtensionContext startAbility, error:${JSON.stringify(error)}');
      } else {
        console.log('FormExtensionContext startAbility success');
      }
    });
  }
};
```

## startAbility

startAbility(want: Want): Promise&lt;void&gt;

Starts an ability. This API uses a promise to return the result.

**System API**: This is a system API.

**System capability**: SystemCapability.Ability.Form

**Parameters**

| Name|                Type              | Mandatory|              Description              |
| ------| --------------------------------- | ---- | -------------------------------------- |
| want| [Want](js-apis-application-want.md) | Yes | Information about the ability to start, such as the bundle name, ability name, and custom parameters.|

**Return value**

| Type         | Description                               |
| ------------ | ---------------------------------- |
| Promise&lt;void&gt; | Promise that returns no value.|

**Example**

```ts
import FormExtensionAbility from '@ohos.app.form.FormExtensionAbility';

export default class MyFormExtensionAbility extends FormExtensionAbility {
  onFormEvent(formId, message) {
    // Call startAbility() when the message event is triggered.
    console.log('FormExtensionAbility onFormEvent, formId:${formId}, message:${message}');
    let want = {
      deviceId: '',
      bundleName: 'com.example.formstartability',
      abilityName: 'EntryAbility',
      parameters: {
        'message': message
      }
    };
    this.context.startAbility(want).then(() => {
      console.info('StartAbility Success');
    }).catch((error) => {
      console.error('StartAbility failed');
    });
  }
};
```
