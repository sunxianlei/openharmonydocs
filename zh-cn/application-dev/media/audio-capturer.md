# 音频采集开发指导

## 简介

AudioCapturer提供了用于获取原始音频文件的方法。开发者可以通过本指导了解应用如何通过AudioCapturer接口的调用实现音频数据的采集。

- **状态检查**：在进行应用开发的过程中，建议开发者通过on('stateChange')方法订阅AudioCapturer的状态变更。因为针对AudioCapturer的某些操作，仅在音频采集器在固定状态时才能执行。如果应用在音频采集器处于错误状态时执行操作，系统可能会抛出异常或生成其他未定义的行为。

## 运作机制

该模块提供了音频采集模块的状态变化示意图。

**图1** 音频采集状态变化示意图

![audio-capturer-state](figures/audio-capturer-state.png)

**PREPARED状态：** 通过调用create()方法进入到该状态。<br>
**RUNNING状态：** 正在进行音频数据播放，可以在prepared状态通过调用start()方法进入此状态，也可以在stopped状态通过调用start()方法进入此状态。<br>
**STOPPED状态：** 在running状态可以通过stop()方法停止音频数据的播放。<br>
**RELEASED状态：** 在prepared和stop状态，用户均可通过release()方法释放掉所有占用的硬件和软件资源，并且不会再进入到其他的任何一种状态了。<br>

## 约束与限制

开发者在进行音频数据采集功能开发前，需要先对所开发的应用配置麦克风权限（ohos.permission.MICROPHONE），配置方式请参见[访问控制授权申请](../security/accesstoken-guidelines.md#配置文件权限声明)。

## 开发指导

详细API含义可参考：[音频管理API文档AudioCapturer](../reference/apis/js-apis-audio.md#audiocapturer8)

1. 使用createAudioCapturer()创建一个全局的AudioCapturer实例。

   在audioCapturerOptions中设置音频采集器的相关参数。该实例可用于音频采集、控制和获取采集状态，以及注册通知回调。 

   ```js
  import audio from '@ohos.multimedia.audio';
  import fs from '@ohos.file.fs';  //便于步骤3 read函数调用
  
  //音频渲染相关接口自测试
  @Entry
  @Component
  struct AudioRenderer {
    @State message: string = 'Hello World'
    private audioCapturer : audio.AudioCapturer;  //供全局调用
  
    async initAudioCapturer(){
      let audioStreamInfo = {
        samplingRate: audio.AudioSamplingRate.SAMPLE_RATE_44100,
        channels: audio.AudioChannel.CHANNEL_1,
        sampleFormat: audio.AudioSampleFormat.SAMPLE_FORMAT_S16LE,
        encodingType: audio.AudioEncodingType.ENCODING_TYPE_RAW
      }
  
      let audioCapturerInfo = {
        source: audio.SourceType.SOURCE_TYPE_MIC,
        capturerFlags: 0 // 0是音频采集器的扩展标志位，默认为0
      }
  
      let audioCapturerOptions = {
        streamInfo: audioStreamInfo,
        capturerInfo: audioCapturerInfo
      }
  
      this.audioCapturer = await audio.createAudioCapturer(audioCapturerOptions);
      console.log('AudioRecLog: Create audio capturer success.');
    }
   ```

2. 调用start()方法来启动/恢复采集任务。

   启动完成后，采集器状态将变更为STATE_RUNNING，然后应用可以开始读取缓冲区。

   ```js
   async  startCapturer() {
     let state = this.audioCapturer.state;
     // Capturer start时的状态应该是STATE_PREPARED、STATE_PAUSED和STATE_STOPPED之一.
     if (state == audio.AudioState.STATE_PREPARED || state == audio.AudioState.STATE_PAUSED ||
     state == audio.AudioState.STATE_STOPPED) {
       await this.audioCapturer.start();
       state = this.audioCapturer.state;
       if (state == audio.AudioState.STATE_RUNNING) {
         console.info('AudioRecLog: Capturer started');
       } else {
         console.error('AudioRecLog: Capturer start failed');
       }
     }
   }
   ```

3. 读取采集器的音频数据并将其转换为字节流。重复调用read()方法读取数据，直到应用准备停止采集。   

   参考以下示例，将采集到的数据写入文件。 

   ```js
   async readData(){
     let state = this.audioCapturer.state;
     // 只有状态为STATE_RUNNING的时候才可以read.
     if (state != audio.AudioState.STATE_RUNNING) {
       console.info('Capturer is not in a correct state to read');
       return;
     }
     const path = '/data/data/.pulse_dir/capture_js.wav'; // 采集到的音频文件存储路径
     let file = fs.openSync(path, 0o2);
     let fd = file.fd;
     if (file !== null) {
       console.info('AudioRecLog: file created');
     } else {
       console.info('AudioRecLog: file create : FAILED');
       return;
     }
     if (fd !== null) {
       console.info('AudioRecLog: file fd opened in append mode');
     }
     let numBuffersToCapture = 150; // 循环写入150次
     let count = 0;
     while (numBuffersToCapture) {
       this.bufferSize = await this.audioCapturer.getBufferSize();
       let buffer = await this.audioCapturer.read(this.bufferSize, true);
       let options = {
         offset: count * this.bufferSize,
         length: this.bufferSize
       }
       if (typeof(buffer) == undefined) {
         console.info('AudioRecLog: read buffer failed');
       } else {
         let number = fs.writeSync(fd, buffer, options);
         console.info(`AudioRecLog: data written: ${number}`);
       }
       numBuffersToCapture--;
       count++;
     }
   }
   ```

4. 采集完成后，调用stop方法，停止录制。

   ```js
   async  StopCapturer() {
     let state = this.audioCapturer.state;
     // 只有采集器状态为STATE_RUNNING或STATE_PAUSED的时候才可以停止
     if (state != audio.AudioState.STATE_RUNNING && state != audio.AudioState.STATE_PAUSED) {
       console.info('AudioRecLog: Capturer is not running or paused');
       return;
     }
   
     await this.audioCapturer.stop();
   
     state = this.audioCapturer.state;
     if (state == audio.AudioState.STATE_STOPPED) {
       console.info('AudioRecLog: Capturer stopped');
     } else {
       console.error('AudioRecLog: Capturer stop failed');
     }
   }
   ```

5. 任务结束，调用release()方法释放相关资源。

   ```js
   async releaseCapturer() {
     let state = this.audioCapturer.state;
     // 采集器状态不是STATE_RELEASED或STATE_NEW状态，才能release
     if (state == audio.AudioState.STATE_RELEASED || state == audio.AudioState.STATE_NEW) {
       console.info('AudioRecLog: Capturer already released');
       return;
     }
   
     await this.audioCapturer.release();
   
     state = this.audioCapturer.state;
     if (state == audio.AudioState.STATE_RELEASED) {
       console.info('AudioRecLog: Capturer released');
     } else {
       console.info('AudioRecLog: Capturer release failed');
     }
   }
   ```

6. （可选）获取采集器相关信息
   
   通过以下代码，可以获取采集器的相关信息。

   ```js
   async getAudioCapturerInfo(){
     // 获取当前采集器状态
     let state = this.audioCapturer.state;
     // 获取采集器信息
     let audioCapturerInfo : audio.AudioCapturerInfo = await this.audioCapturer.getCapturerInfo();
     // 获取音频流信息
     let audioStreamInfo : audio.AudioStreamInfo = await this.audioCapturer.getStreamInfo();
     // 获取音频流ID
     let audioStreamId : number = await this.audioCapturer.getAudioStreamId();
     // 获取纳秒形式的Unix时间戳
     let audioTime : number = await this.audioCapturer.getAudioTime();
     // 获取合理的最小缓冲区大小
     let bufferSize : number = await this.audioCapturer.getBufferSize();
   }
   ```

7. （可选）使用on('markReach')方法订阅采集器标记到达事件，使用off('markReach')取消订阅事件。

    注册markReach监听后，当采集器采集的帧数到达设定值时，会触发回调并返回设定的值。
   
    ```js
    async markReach(){
      this.audioCapturer.on('markReach', 10, (reachNumber) => {
        console.info('Mark reach event Received');
        console.info(`The Capturer reached frame: ${reachNumber}`);
      });
      this.audioCapturer.off('markReach'); // 取消markReach事件的订阅，后续将无法监听到“标记到达”事件
    }
    ```

8. （可选）使用on('periodReach')方法订阅采集器区间标记到达事件，使用off('periodReach')取消订阅事件。

    注册periodReach监听后，**每当**采集器采集的帧数到达设定值时，会触发回调并返回设定的值。
   
    ```js
    async periodReach(){
      this.audioCapturer.on('periodReach', 10, (reachNumber) => {
        console.info('Period reach event Received');
        console.info(`In this period, the Capturer reached frame: ${reachNumber}`);
      });
      this.audioCapturer.off('periodReach'); // 取消periodReach事件的订阅，后续将无法监听到“区间标记到达”事件
    }
    ```

9. 如果应用需要在采集器状态更新时进行一些操作，可以订阅该事件，当采集器状态更新时，会受到一个包含有事件类型的回调。

    ```js
    async stateChange(){
      this.audioCapturer.on('stateChange', (state) => {
        console.info(`AudioCapturerLog: Changed State to : ${state}`)
        switch (state) {
          case audio.AudioState.STATE_PREPARED:
            console.info('--------CHANGE IN AUDIO STATE----------PREPARED--------------');
            console.info('Audio State is : Prepared');
            break;
          case audio.AudioState.STATE_RUNNING:
            console.info('--------CHANGE IN AUDIO STATE----------RUNNING--------------');
            console.info('Audio State is : Running');
            break;
          case audio.AudioState.STATE_STOPPED:
            console.info('--------CHANGE IN AUDIO STATE----------STOPPED--------------');
            console.info('Audio State is : stopped');
            break;
          case audio.AudioState.STATE_RELEASED:
            console.info('--------CHANGE IN AUDIO STATE----------RELEASED--------------');
            console.info('Audio State is : released');
            break;
          default:
            console.info('--------CHANGE IN AUDIO STATE----------INVALID--------------');
            console.info('Audio State is : invalid');
            break;
        }
      });
    }
    ```