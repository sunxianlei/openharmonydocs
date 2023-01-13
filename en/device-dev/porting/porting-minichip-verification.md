# Porting Verification


After the OpenHarmony chip is ported, conduct the OpenHarmony compatibility test and chip SDK function test to obtain certification. Detecting defects in the development process can improve code quality.


## Conducting the OpenHarmony Compatibility Test

The OpenHarmony compatibility test is included in the X Test Suite (XTS), a set of OpenHarmony certification test suites. For details, see [DFX](https://gitee.com/openharmony/docs/blob/master/en/readme/dfx.md).

1. Add the test subsystem and the xts_acts component.
   Add the following code to the **vendor/xxx/xxx/config.json** file:

     
   ```
   {
     "subsystem": "test",
     "components": [
       { "component": "xts_acts", "features":[] },
       { "component": "xts_tools", "features":[] }
     ]
   }
   ```

2. Link the .a library generated by the XTS.
   In the linking options, link the **libmodule_ActsXxxTest.a** library in the **out/MyBoard/MyProduct/libs** directory in the mode of **-lmodule_ActsXxxTest**. The sample code is as follows:

     
   ```
   "-Wl,--whole-archive",
   ......
   "-lhctest",
   "-lbootstrap",
   "-lbroadcast",
   "-lmodule_ActsBootstrapTest",
   "-lmodule_ActsCMSISTest",
   "-lmodule_ActsDfxFuncTest",
   "-lmodule_ActsParameterTest",
   "-lmodule_ActsSamgrTest",
   "-lmodule_ActsSecurityDataTest",
   ......
   "-Wl,--no-whole-archive",
   ```

3. Modify the code based on the test report.
   Burn the files generated after compilation to the development board and use the serial port tool to view the XTS test report. If any test item fails, modify the code as needed.

   During fault locating, you can comment out unnecessary test items in the **test/xts/acts/build_lite/BUILD.gn** file.

     
   ```
   if (ohos_kernel_type == "liteos_m") {
     all_features += [
       "//test/xts/acts/communication_lite/lwip_hal:ActsLwipTest",
       "//test/xts/acts/communication_lite/softbus_hal:ActsSoftBusTest",
       "//test/xts/acts/communication_lite/wifiservice_hal:ActsWifiServiceTest",
       "//test/xts/acts/utils_lite/file_hal:ActsUtilsFileTest",
       "//test/xts/acts/startup_lite/syspara_hal:ActsParameterTest",
       "//test/xts/acts/iot_hardware_lite/iot_controller_hal:ActsWifiIotTest",
       "//test/xts/acts/kernel_lite/kernelcmsis_hal:ActsCMSISTest",
       "//test/xts/acts/utils_lite/kv_store_hal:ActsKvStoreTest",
       "//test/xts/acts/security_lite/datahuks_hal:ActsSecurityDataTest",
       "//test/xts/acts/hiviewdfx_lite/hilog_hal:ActsDfxFuncTest",
       "//test/xts/acts/distributed_schedule_lite/samgr_hal:ActsSamgrTest",
       "//test/xts/acts/update_lite/updater_hal:ActsUpdaterFuncTest",
       "//test/xts/acts/startup_lite/bootstrap_hal:ActsBootstrapTest",
     ]
   }
   ```

> ![icon-caution.gif](public_sys-resources/icon-caution.gif) **CAUTION**
> 1. XTS automatically runs the test after **OHOS_SystemInit()** is called.
> 
> 2. You must add code between "-Wl,--whole-archive" and "-Wl,--no-whole-archive". Otherwise, the link fails.
> 
> During the XTS test, the following static libraries must be linked:
> 
>   
> ```
> "-lhctest",
> "-lbootstrap",
> "-lbroadcast",
> ```


## Conducting the Chip SDK Function Test

Verify the chip SDK functions, such as Wi-Fi, Bluetooth, and OTA.