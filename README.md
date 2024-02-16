# ffmpeg_notes

## Concatenate a list of videos into one

```
ffmpeg -f concat -safe 0 -i tojoin.txt -c copy output.mp4
```
    -  Format of tojoin.txt:
        file 'file0.MP4'
        file 'file1.MP4'
        file 'etc..

##  Scale down 4k video to

### / 2.7k / 2704p

```
ffmpeg -i output.mp4 -vf scale=2704:1520 -c:v libx264 -crf 20 -preset slow smaller_2704p.mp4
```

### 1440p

```
ffmpeg -i output.mp4 -vf scale=1920:1440 -c:v libx264 -crf 20 -preset slow smaller_1440p.mp4
```

### 1080p

```
ffmpeg -i output.mp4 -vf scale=1920:1080 -c:v libx264 -crf 20 -preset slow smaller_1080p.mp4
```

### 720p

```
ffmpeg -i output.mp4 -vf scale=1280:720 -c:v libx264 -crf 20 -preset slow smaller_720p.mp4
```

## Convert files in directory

```
for %f in ("*.mp4") do c:\ffmpeg\bin\ffmpeg -i "%f" -vf scale=1920:1080 -c:v libx264 -crf 20 -preset slow "converted%~f"
```

## Make a video from image serie

```
c:\ffmpeg\bin\ffmpeg.exe -r 10 -f image2 -s 1130x620 -i sa_%02d_00.png -vcodec libx264 -crf 5  -pix_fmt yuv420p test.mp4
c:\ffmpeg\bin\ffmpeg.exe -i sa_1500.mp4 -i crop.mp4 -filter_complex "overlay=250:main_h-overlay_h-0" combined15.mp4
c:\ffmpeg\bin\ffmpeg.exe -i test1.mp4 -filter:v "crop=300:300:0:70" -c:a copy crop.mp4
```