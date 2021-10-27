# 常用命令

## 一、基本信息查询

|-version|查看版本|-formats|查看可用的格式|
|:--|:--|:--|:--|
|-demuxers|查看可用的demuxers|-protocols|查看可用的协议|
|-muxers|查看可用的muxers|-filters|查看可用的过滤器|
|-devices|查看可用的设备|-pix_fmts|查看可用的像素格式|
|-codecs|查看所有编解码器|-sample_fmts|查看可用的采样格式|
|-decoders|查看可用的解码器|-layouts|查看channel名|
|-encoders|查看所有编码器|-colors|查看识别的颜色名称|
|-bsfs|查看比特流filter|-|-|

## 二、录制

### 屏幕录制命令

```shell
ffmpeg -f avfoundation -i 1 -r 30 out.yuv
```

`-f` 指定使用Mac avfoundation 采集数据

`-i` 指定从哪儿采集数据，是设备索引。0摄像头 1屏幕

`-r` 指定帧率

`yuv` 原始数据格式

```shell
# Record info
# Output #0, rawvideo, to 'out.yuv':
#   Metadata:
#     Stream #0:0: Video: rawvideo (UYVY / 0x59565955), uyvy422, 3584x2240, q=2-31, 3853516 kb/s, 30 fps, 30 tbn, 30 tbc
# play
ffplay -video_size 3584x2240 -pixel_format uyvy422 out.yuv
```

#### Mac devices list

```shell
ffmpeg -f avfoundation -list_devices true -i ""
```

```shell
# output
[AVFoundation input device @ 0x7fa9e00000c0] AVFoundation video devices:
[AVFoundation input device @ 0x7fa9e00000c0] [0] FaceTime HD Camera (Built-in)
[AVFoundation input device @ 0x7fa9e00000c0] [1] Capture screen 0
[AVFoundation input device @ 0x7fa9e00000c0] AVFoundation audio devices:
[AVFoundation input device @ 0x7fa9e00000c0] [0] MacBook Pro Microphone
: Input/output error
```

### 音频录制

```shell
ffmpeg -f avfoundation -i :0 out.wav
```

`:0` 0为音频设备，`:`前指定视频设备

## 三、分解/复用

### 多媒体格式转换

```shell
ffmpeg -i InputVideo.mkv -vcodec copy -acodec copy OutputVideo.mp4
```

`-i`: 输入文件

`-vcodec copy`: 视频编码处理方式

`-acodec copy`: 音频编码处理方式

## 四、处理原始数据

## 五、裁剪与合并

## 六、图片/视频互转

## 七、直播相关

## 八、各种滤镜

### delogo 去Logo水印

```shell
# video size 1920x1080, logo x:1670 y:50 width:176 height:72
ffmpeg % ffmpeg -i InputVideo.mp4 -vf delogo=x=1670:y=50:w=176:h=72 OutputVideo.mp4
```
