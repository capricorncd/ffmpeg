# Automator Mac

Launchpad -> Other -> Automator

### toMp3

```shell
# /bin/zsh
for f in "$@"
do
  fname=$(basename "$f")
  fpath=$(dirname "$f")
  if [ ! -d "${fpath}/mp3" ]; then
    mkdir -p "${fpath}/mp3"
  fi
  /usr/local/Cellar/ffmpeg/5.0/bin/ffmpeg -i "$f" "$fpath"/mp3/${fname%.*}.mp3
done
```

### 2x mp3

```shell
# /bin/zsh
for f in "$@"
do
  fname=$(basename "$f")
  fpath=$(dirname "$f")
  if [ ! -d "${fpath}/mp3-2x" ]; then
    mkdir -p "${fpath}/mp3-2x"
  fi
  /usr/local/Cellar/ffmpeg/5.0/bin/ffmpeg -i "$f" -af atempo=2.0 "$fpath"/mp3-2x/${fname%.*}.mp3
done
```

### FlvToMp4

```shell
# /bin/zsh
for f in "$@"
do
  fname=$(basename "$f")
  fpath=$(dirname "$f")
  if [ ! -d "${fpath}/mp4" ]; then
    mkdir -p "${fpath}/mp4"
  fi
  /usr/local/Cellar/ffmpeg/5.0/bin/ffmpeg -i "$f" -c copy "$fpath"/mp4/${fname%.*}.mp4
done
```

### toAAC

```shell
# /bin/zsh
for f in "$@"
do
  fname=$(basename "$f")
  fpath=$(dirname "$f")
  if [ ! -d "${fpath}/audio" ]; then
    mkdir -p "${fpath}/audio"
  fi
  /usr/local/Cellar/ffmpeg/5.0/bin/ffmpeg -i "$f" -c copy "$fpath"/audio/${fname%.*}.aac
done
```
