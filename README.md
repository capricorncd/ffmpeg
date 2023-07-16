# FFmpeg

A complete, cross-platform solution to record, convert and stream audio and video.

Converting video and audio has never been so easy.

```shell script
$ ffmpeg -i input.mp4 output.avi
```

https://www.ffmpeg.org/

## Notes

[Notes](./notes/)

## 五、裁剪与合并

### 裁剪

```shell
# How to Cut Video Using FFmpeg
ffmpeg -i input.mp4 -ss 00:00:00 -t 10:00:00 -c copy out.mp4
ffmpeg -i input.mp4 -ss 00:00:00 -t 10 out.ts
# -to hh:mm:ss
# ffmpeg -i input.mp4 -ss 00:03:09 -to 00:19:01 -acodec copy -vcodec copy out.mp4
ffmpeg -i input.mp4 -ss 00:03:09 -to 00:19:01 -c copy out.mp4
```

```shell
# 按5小时一段分割视频
ffmpeg \
  -i input.mp4 \
  -c copy \
  -map 0 \
  -segment_time 05:00:00 \
  -f segment \
  -reset_timestamps 1 \
  output%03d.mp4
```

### 合并

```shell
# 合并
ffmpeg -f concat -i inputs.txt -vcodec copy -acodec copy out.mp4
```

```text
# inputs.txt
# file filename
file 1.ts
file 2.ts
```

Error: `[concat @ 0x0000000] Unsafe file name someFileName`

```shell
# -safe 0
ffmpeg -f concat -safe 0 -i inputs.txt -vcodec copy -acodec copy out.mp4
# or
ffmpeg -f concat -safe 0 -i inputs.txt -c copy out.mp4
```

[More](./notes/)


