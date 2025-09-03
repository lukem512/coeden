# coeden
Coeden tree care website.

## Images

Thumbnails are 500px wide and encoded at 80% quality using GIMP.

## Video encoding

Crop the video to length:

```sh
./ffmpeg -ss 00:00:07 -to 00:00:25 -i input.mp4 -c copy trimmed.mp4
```

Resize the trimmed video and output it as WEBM for speed:

```sh
./ffmpeg -i trimmed.mp4 -an -vf "scale=1280:-1,fps=24,crop=in_w:450:0:(in_h-450)/2" -c:v libsvtav1 -crf 40 -preset 6 -b:v 0  hero.webm
```

Generate an MP4 using the older H.264 codec for Safari and iOS:

```sh
./ffmpeg -i trimmed.mp4 -an -vf "scale=1280:-1,fps=24,crop=in_w:450:0:(in_h-450)/2" -c:v libx264 -preset veryslow -crf 40 hero.mp4
```

Finally, extract the first frame in case it is needed as a poster or pre-load:

```sh
./ffmpeg -i hero.webm -vf "select=eq(n\,0)" -q:v 3 hero.jpg
```