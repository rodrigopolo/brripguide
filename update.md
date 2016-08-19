# Update 2016

## 3D SBS Video Encoding
To avoid the complexities of using AviSynth for the 3D SBS Video Encoding I switched to FRIM Decoder, a free MVC-3D command-line tool that converts the two streams into a side-by-side YUV stream, and instead of using X264 I switched directly to FFmpeg which now is simpler to use, I use a custom FFmpeg build that has almost all codecs necessary, so download FFmpeg, the libfdk-aac encoder and FRIM from the following links, BTW i use the X264 versions:


* [FFmpeg and libfdk-aac](http://oss.netfarm.it/mplayer/)
* [FRIM](http://www.videohelp.com/software/FRIM)

To install, extract the downloaded files and put all `.exe` and `.dll` in the `c:\brdsoft` directory that is already added to your system path [as showed on the encoding guide](guide_en.md#system-preparation).

To encode the `left.h264` and `right.h264` files into a single side-by-side H.264 MP4 video file I use `FRIMDecode64` and `FRIMDecode64`, here is the command explained line by line, **Do not copy/paste this command** it is just so you understand what it is doing.

```
FRIMDecode64 								// Invoque/run FRIMDecode64
-i:mvc 										// MVC-3D input flag
left.h264 									// The left eye input file
right.h264 									// The right eye input file
-sbs 										// The Side-by-Side flag
-o - 										// Send the output to a pipe
| 											// pipe
FFmpeg 										// Invoque/run FFmpeg
-y 											// The overwrite output files without asking flag
-f rawvideo 								// The raw video input flag
-s:v 3840x1080 								// The size of the raw input file, double width because it is SbS
-r 24000/1001 								// The frame rate
-i - 										// The input flag telling it is from a pipe
-pix_fmt yuv420p 							// Set the pixel format to YUV 4:2:0 which is the one H.264 use
-vf "scale=1920:1080,crop=1920:800:0:140" 	// Video filter to resize the video to half the width and crop the letterbox
-c:v libx264 								// Set LibX264 as the encoding library
-preset medium 								// Set the preset for the X264 library
-crf 22 									// Set the CRF quality to 22
-an 										// The outpot has NO audio
movie.mp4 									// The output file
```

And here is the command you use to encode the video without explaination, change values that could need adjustments, like the video size, frame rate, cropping, etc.
```
FRIMDecode64 -i:mvc left.h264 right.h264 -sbs -o - | FFmpeg -y -f rawvideo -s:v 3840x1080 -r 24000/1001 -i - -pix_fmt yuv420p -vf "scale=1920:1080,crop=1920:800:0:140" -c:v libx264 -preset medium -crf 22 -an movie.mp4
```

After the encoding proccess you'll have a half-side-by-side H.264/MP4 file ready to be combined with your other movie tracks as described on the [main encoding guide](guide_en.md).

Just as an extra note, if you want to encode just the right side, here is what I did:
```
FRIMDecode64 -i:mvc left.h264 right.h264 -o NUL -o - | FFmpeg -y -f rawvideo -s:v 1920x1080 -r 24000/1001 -i - -pix_fmt yuv420p -c:v libx264 -preset medium -crf 22 -an right_side.mp4
```

## Subtitles
Forget about SubExtractor and SupRip, use **Subtitle Edit** instead, it can do anything related to subtitles, OCR from many formats, it supports multiple languages, it has dictionaries, it is open source and FLOSS, you can download it from the following link:

https://github.com/SubtitleEdit/subtitleedit/releases

To create the SRT subtitles from a Blu-ray disc:
* Open Subtitle Edit.
* Click in the `File` menu.
* Select the `Import/OCR Blu-ray (.sup) subtitle file` menu.
* Select your `.sup` file.
* On the `Import/OCR Blu-ray (.sup) subtitle` window, select your OCR method, I use `OCR via Tesseract`.
* Then, select the subtitle language, if your language isn't installed, you can install it clicking on the `...` button right in the `Language` selection.
* if you want to enable/disable the `Italic` and `Music symbol` options click on the checkboxes.
* In the `OCR auto correction / spell checking` select which dictionary you want to use, again, you can download other languages right from the `...` button.
* Check the `Fix OCR errors` option.
* Uncheck the `Prompt for unknown words` option, unless you want to be anoyed trough all the OCR proccess.
* Check the `Try to guess unknown words` option, it is very reliable.
* Check the `Auto break paragraph if more than two lines` option.
* And to start the proccess, click on the **`Start OCR`** button.
* See how the magic happens, glorious automatic OCR, wait until it ends.
* When the OCR proccess ends it stays on the last subtitle, click the `Ok` button.
* Save your SRT file, use `Unicode (UTF-8)` Encoding.

If you find this information useful, you can support by donating on [this link](http://rodrigopolo.com/about/wp-stream-video/donate).