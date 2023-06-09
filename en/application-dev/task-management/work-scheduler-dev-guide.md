# Work Scheduler Development

## When to Use

If your application needs to execute a non-real-time task or a persistent task, for example, data learning, you can harness the Work Scheduler mechanism, which will schedule the task based on the storage space, power consumption, temperature, and more when the preset conditions are met. Your application must implement the callbacks provided by [WorkSchedulerExtensionAbility](./workscheduler-extensionability.md) for Work Scheduler tasks.
For details about the restrictions, see [Restrictions on Using Work Scheduler](./background-task-overview.md#restrictions-on-using-work-scheduler).

## Available APIs

**Table 1** Major workScheduler APIs

API                                                   |     Description                           
---------------------------------------------------------|-----------------------------------------
startWork(work: WorkInfo): void; | Starts a Work Scheduler task.
stopWork(work: WorkInfo, needCancel?: boolean): void;        | Stops a Work Scheduler task.
getWorkStatus(workId: number, callback: AsyncCallback\<WorkInfo>): void;| Obtains the status of a Work Scheduler task. This API uses an asynchronous callback to return the result.
getWorkStatus(workId: number): Promise\<WorkInfo>; | Obtains the status of a Work Scheduler task. This API uses a promise to return the result.
obtainAllWorks(callback: AsyncCallback\<void>): Array\<WorkInfo>;| Obtains all the Work Scheduler tasks. This API uses an asynchronous callback to return the result.
obtainAllWorks(): Promise<Array\<WorkInfo>>;| Obtains all the Work Scheduler tasks. This API uses a promise to return the result.
stopAndClearWorks(): void;| Stops and clears all the Work Scheduler tasks.
isLastWorkTimeOut(workId: number, callback: AsyncCallback\<void>): boolean;| Checks whether the last execution of the specified task has timed out. This API uses an asynchronous callback to return the result. It is applicable to repeated tasks.
isLastWorkTimeOut(workId: number): Promise\<boolean>;| Checks whether the last execution of the specified task has timed out. This API uses a promise to return the result. It is applicable to repeated tasks.

**Table 2** WorkInfo parameters

For details about the restriction on configuring **WorkInfo**, see [Restrictions on Using Work Scheduler](./background-task-overview.md#restrictions-on-using-work-scheduler).

Name| Type|Description                      
---------------------------------------------------------|-----------------------------------------|---------------------------------------------------------
workId| number | ID of the Work Scheduler task. Mandatory.
bundleName| string | Bundle name of the Work Scheduler task. Mandatory.
abilityName| string | Name of the ability to be notified by a Work Scheduler callback. Mandatory.
networkType  | [NetworkType](../reference/apis/js-apis-resourceschedule-workScheduler.md#networktype) | Network type.
isCharging| boolean | Whether the device is charging.
chargerType| [ChargingType](../reference/apis/js-apis-resourceschedule-workScheduler.md#chargingtype) | Charging type.
batteryLevel| number | Battery level.
batteryStatus| [BatteryStatus](../reference/apis/js-apis-resourceschedule-workScheduler.md#batterystatus) | Battery status.
storageRequest| [StorageRequest](../reference/apis/js-apis-resourceschedule-workScheduler.md#storagerequest) |Storage status.
isRepeat| boolean |Whether the task is repeated.
repeatCycleTime| number |Repeat interval.
repeatCount | number|Number of repeat times.
parameters | {[key: string]: number | string | boolean} |Carried parameters.

**Table 3** Work Scheduler callbacks

API                                                   |     Description                           
---------------------------------------------------------|-----------------------------------------
onWorkStart(work: WorkInfo): void | Called when the Work Scheduler task starts.
onWorkStop(work: WorkInfo): void | Called when the Work Scheduler task stops.

### How to Develop

1. Import the modules.

   Import the **workScheduler** module.
   
   ```js
   import workScheduler from '@ohos.resourceschedule.workScheduler';
   ```

   Import the **WorkSchedulerExtensionAbility** module.
   ```js
   import WorkSchedulerExtensionAbility from    '@ohos.WorkSchedulerExtensionAbility';
   ```

2. Develop an ExtensionAbility to execute a Work Scheduler task. For details about the ExtensionAbility, see [ExtensionAbility Component Overview](../application-models/extensionability-overview.md) and [WorkSchedulerExtensionAbility Development](./workscheduler-extensionability.md).

   ```ts
   import WorkSchedulerExtensionAbility from '@ohos.WorkSchedulerExtensionAbility';

   export default class MyExtension extends WorkSchedulerExtensionAbility {
       onWorkStart(workInfo) {
           console.log('MyWorkSchedulerExtensionAbility onWorkStart' + JSON.stringify(workInfo));
       }
       onWorkStop(workInfo) {
           console.log('MyWorkSchedulerExtensionAbility onWorkStop' + JSON.stringify(workInfo));
       }
   }
   ```


3. Start a Work Scheduler task.

   ```ts
   import workScheduler from '@ohos.resourceschedule.workScheduler';
    
   let workInfo = {
       workId: 1,
       batteryStatus:workScheduler.BatteryStatus.BATTERY_STATUS_LOW,
       isRepeat: false,
       isPersisted: true,
       bundleName: "com.example.myapplication",
       abilityName: "MyExtension",
       parameters: {
         mykey0: 1,
         mykey1: "string value",
         mykey2: true,
         mykey3: 1.5
     }
   }
   try{
     workScheduler.startWork(workInfo);
     console.info('workschedulerLog startWork success');
   } catch (error) {
     console.error(`workschedulerLog startwork failed. code is       ${error.code} message is ${error.message}`);
   }
   ```


4. Stop the Work Scheduler task.

   ```ts
   import workScheduler from '@ohos.resourceschedule.workScheduler';

   let workInfo = {
       workId: 1,
       batteryStatus:workScheduler.BatteryStatus.BATTERY_STATUS_LOW,
       isRepeat: false,
       isPersisted: true,
       bundleName: "com.example.myapplication",
       abilityName: "MyExtension",
       parameters: {
         mykey0: 1,
         mykey1: "string value",
         mykey2: true,
         mykey3: 1.5
       }
   }
   try{
       workScheduler.stopWork(workInfo, false);
       console.info('workschedulerLog stopWork success');
   } catch (error) {
       console.error(`workschedulerLog stopWork failed. code is    ${error.code} message is ${error.message}`);
   }
   
   ```


5. Obtain a specified Work Scheduler task.

   ```ts
   try{
     workScheduler.getWorkStatus(50, (error, res) => {
       if (error) {
         console.error(`workschedulerLog getWorkStatus failed. code is    ${error.code} message is ${error.message}`);
       } else {
         for (let item in res) {
           console.info(`workschedulerLog getWorkStatus success, ${item}    is: ${res[item]}`);
         }
       }
     });
   } catch (error) {
     console.error(`workschedulerLog getWorkStatus failed. code is    ${error.code} message is ${error.message}`);
   }
   ```

6. Obtain all the Work Scheduler tasks.

   ```ts
   try{
     workScheduler.obtainAllWorks((error, res) =>{
       if (error) {
         console.error(`workschedulerLog obtainAllWorks failed. code is    ${error.code} message is ${error.message}`);
       } else {
         console.info(`workschedulerLog obtainAllWorks success, data is:    ${JSON.stringify(res)}`);
       }
     });
   } catch (error) {
     console.error(`workschedulerLog obtainAllWorks failed. code is    ${error.code} message is ${error.message}`);
   }
   ```

7. Stop and clear all the Work Scheduler tasks.

   ```ts
   try{
     workScheduler.stopAndClearWorks();
     console.info(`workschedulerLog stopAndClearWorks success`);
   } catch (error) {
     console.error(`workschedulerLog stopAndClearWorks failed. code is    ${error.code} message is ${error.message}`);
   }
   ```

8. Check whether the last execution of a specified Work Scheduler task has timed out.

   ```ts
   try{
     workScheduler.isLastWorkTimeOut(500, (error, res) =>{
       if (error) {
         onsole.error(`workschedulerLog isLastWorkTimeOut failed. code   is ${error.code} message is ${error.message}`);
       } else {
         console.info(`workschedulerLog isLastWorkTimeOut success, data is: ${res}`);
       }
     });
   } catch (error) {
     console.error(`workschedulerLog isLastWorkTimeOut failed. code is ${error.code} message is ${error.message}`);
   }
   ```
