# Automator Mac

Launchpad -> Other -> Automator

### toMp3

```shell
# /bin/zsh
for f in "$@"
do
  fname=$(basename "$f")
  fpath=$(dirname "$f")
  /usr/local/Cellar/ffmpeg/5.0/bin/ffmpeg -i "$f" "$fpath"/${fname%.*}.mp3
done
```

[file](../files/Automator/)

### 2x mp3

```shell
# /bin/zsh
for f in "$@"
do
  fname=$(basename "$f")
  fpath=$(dirname "$f")
  /usr/local/Cellar/ffmpeg/5.0/bin/ffmpeg -i "$f" -af atempo=2.0 "$fpath"/${fname%.*}2x.mp3
done
```

[file](../files/Automator/)

### FlvToMp4

```shell
# /bin/zsh
for f in "$@"
do
  fname=$(basename "$f")
  fpath=$(dirname "$f")
  /usr/local/Cellar/ffmpeg/5.0/bin/ffmpeg -i "$f" -c copy "$fpath"/${fname%.*}.mp4
done
```

[file](../files/Automator/)

### toAAC

```shell
# /bin/zsh
for f in "$@"
do
  fname=$(basename "$f")
  fpath=$(dirname "$f")
  /usr/local/Cellar/ffmpeg/5.0/bin/ffmpeg -i "$f" -c copy "$fpath"/${fname%.*}.aac
done
```

[file](../files/Automator/)
