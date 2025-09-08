# Use VA-API to encode with `ffmpeg`

This is a very convenient speedup, my laptop with Intel Core i7-10510 and integrated
CometLake-U GT2 UHD graphics is able to encode at 5x the frame rate, while it only achieved
around 0.3x speed using CPU encoders.

The specific codec support varies, I found that this laptop is capable of encoding using
[h265 (a.k.a. HEVC)][00], and that provides a fairly small output file size with decent quality.

The command that I use is:

```
ffmpeg \
  -vaapi_device /dev/dri/renderD218 \
  - i <input_file> \
  -vf 'format=nv12,hwupload' \
  -c:v hevc_vaapi \
  -profile:v main \
  -rc_mode CQP \
  -global_quality 28 \
  <output_file>
```

[//]: # ( ------------------- references below this line ------------------- )

To be honest, I don't fully understand all of the options, here is more information from `ffmpeg`
docs about [VA-API][01], and here is a [blog post][02] and other [StackOverflow][03] thread.

[00]: https://en.wikipedia.org/wiki/High_Efficiency_Video_Coding
[01]: https://trac.ffmpeg.org/wiki/Hardware/VAAPI
[02]: https://www.tauceti.blog/posts/linux-ffmpeg-amd-5700xt-hardware-video-encoding-hevc-h265-vaapi/
[03]: https://stackoverflow.com/questions/26000606/how-do-you-get-ffmpeg-to-encode-with-vaapi
