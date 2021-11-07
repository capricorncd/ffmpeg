# 常用命令

https://www.ffmpeg.org/

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
# video only
ffmpeg -i InputVideo.mp4 -an -vcodec copy OutputVideo.h264
# audio only
ffmpeg -i InputVideo.mp4 -vn -acodec copy OutputAudio.aac
```

`-i`: 输入文件

`-vcodec copy`: 视频编码处理方式

`-acodec copy`: 音频编码处理方式

`-an`: 无音频

`-vn`: 无视频

## 四、处理原始数据

```shell
ffmpeg -i input.mp4 -an -c:v rawvideo -pix_fmt yuv420p out.yuv
```

### 提取PCM数据

```shell
ffmpeg -i input.mp4 -vn -ar 44100 -ac2 -f s16le out.pcm
# play
ffplay -ar 44100 -ac 2 -f s16le out.pcm
```

## 五、裁剪与合并

```shell
# 裁剪
ffmpeg -i input.mp4 -ss 00:00:00 -t 10 out.ts
```

```shell
# 合并
ffmpeg -f concat -i inputs.txt out.mp4
```

```text
# inputs.txt
# file filename
file 1.ts
file 2.ts
```

## 六、图片/视频互转

```shell
# to image
ffmpeg -i input.mp4 -r 1 -f image2 image-%3d.jpg
```

```shell
# to video
ffmpeg -i image-%3d.jpg OutImage.mp4
# ffmpeg -f image2 -r 1 -i image-%3d.jpg OutImage.mp4
# ffmpeg -f image2 -r 1 -i image-%3d.jpg -loop 1 -pix_fmt yuv420p -video_size 1920x1080 -r 10 -c:v libx264 OutImage.mp4
```

## 七、直播相关

## 八、各种滤镜

https://www.ffmpeg.org/ffmpeg-filters.html

```shell
ffmpeg -i input.mov -vf crop=in_w-200:in_h-200 -c:v libx264 -c:a copy out.mp4
```

`-vf`: 视频滤镜 crop

`crop`: crop=out_w:out_h:x:y

`in_w-200`: 视频宽度`减去`200

### delogo 去Logo水印

```shell
# video's size, width:1920 height:1080
# logo's postion and size, x:1670 y:50 width:176 height:72
ffmpeg % ffmpeg -i InputVideo.mp4 -vf delogo=x=1670:y=50:w=176:h=72 OutputVideo.mp4
```
