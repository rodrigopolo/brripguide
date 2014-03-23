# Ultimate Blu-ray Disc (3D) Ripping Guide

### Purpose
The purpose of this guide is to share the knowhow of video encoding so you can create a backup copy of your own Blu-ray Discs and watch your movies on a wider range of devices that doesn't support or have a Blu-ray Disc drive using almost only free/libre software.

**This guide does not encourage, support or endorse piracy in any way**, we are not responsible in any way on what anyone can do with this information, all the information here is provided "as is", without warranty of any kind, express or implied, including but not limited to the warranties of merchantability, fitness for a particular purpose and noninfringement. In no event shall the authors or copyright holders be liable for any claim, damages or other liability, whether in an action of contract, tort or otherwise, arising from, out of or in connection with this guide or the use or other dealings in the guide.

### Format goals
  * MKV AVCHD - format for most Smart TVs.
  * M4V AVCHD - for iTunes / Apple TV 3.
  * MKV AVCHD SBS 3D - for SBS compatible hardware, software and Smart TVs.

Yes, there are plenty of tools that can achieve the same goals with a single click, but this guide is designed to give you full control over every single step of the encoding process, achieve higher quality, get smaller and more compatible files, use the best tools available and almost 99% free/libre software, no unwanted extras included in the files, but most important, this guide will show you techniques that are bullet proof and 100% tested, the encoded files will work great on any Smart TV, Apple TV, XBMC, Stereoscopic Player, PowerDVD, etc. showing perfect results and quality.

### System Requirements
  * **Windows**: I'm running all this software on Windows 8.1 x64 on a MacBook Pro Retina, sadly, almost of this software only runs on Windows.
  * **A Blu-ray Disc Drive**: I'm using a USB External Blu-ray Disc Drive, there are plenty of those in [Amazon](http://amzn.to/PSc9Xh)
  * **OS X**: For those who want to have an iTunes / Apple TV Compatible format.
  * **Free disk space**: at last 50GiB

### Source
The Blu-ray Disc title I'm using for this guide is "[Thor: The Dark World (2013)](http://www.amazon.com/dp/B00HERGM86)" which is a 3D Blu-ray I own.


### Software Required
* [AnyDVD HD](http://www.slysoft.com/en/anydvdhd.html): For Blu-ray Disc decryption - commercial.
* [HandBrake](http://handbrake.fr/): For easy video encoding - free,
  [Direct Download](http://handbrake.fr/rotation.php?file=HandBrake-0.9.9-1_x86_64-Win_GUI.exe).
* [eac3to](http://www.videohelp.com/tools/eac3to): For media information, demuxing and audio encoding - free,
  [Direct Download](http://www.videohelp.com/download/eac3to327.zip).
* [SubExtractor](http://www.videohelp.com/tools/SubExtractor): To convert `.bup` subtitles into `.srt` subtitles (OCR) - free,
  [Direct Download](http://www.videohelp.com/download/SubExtractor1031.zip).
* [SupRip](http://www.videohelp.com/tools/SupRip): To convert `.bup` subtitles into `.srt` subtitles (OCR) - free,
  [Direct Download](http://www.videohelp.com/download/suprip-1.16.rar).
* [MKVToolNix](http://www.fosshub.com/MKVToolNix.html): To mux (join) all the track together - free,
  [Direct Download](http://www.fosshub.com/download/mkvtoolnix-amd64-6.8.0.7z).

### Steps

To convert a Blu-ray Disc into a MKV or M4V video file we have to do the following steps:

1. [Install all the software necessary](#system-preparation).
2. [Extract all the desired tracks](#demuxing).
3. Encode and convert all the tracks one by one.
  1. [Video Encoding](#video-encoding)
  2. [Audio Encoding](#audio-encoding)
  3. [Subtitles OCR](#subtitles)
4. [Join all the encoded and converted tracks into a single file (mux or remux)](#remuxing).

## System Preparation
First, we need to have all the necessary tools for video encoding, demuxing and muxing correctly installed.

1. Install AnyDVD HD to have unencrypted access to your Blu-ray Disc.
2. Install HandBrake.
3. Create a folder to store all the free software that doesn't require installation, for this guide I'm going to use the folder `c:\brdsoft`.
4. Add the `c:\brdsoft` to your system path:
  1. Right click on the bottom left corner of Windows to access the menu and then click "System":  
  ![Windows Menu](img/01-menu.png)
  2. On the "System" window click on the "Advanced system settings":  
  ![System](img/02-system.png)
  3. On the "System Properties" windows, click on the "Environment Variables" button:  
  ![System Properties](img/03-System_Properties.png)
  4. On the "Environment Variables" windows, edit the "PATH" on the "User variables" list and add the path   where you'll put the software with a `;` at the beginning `;C:\brdsoft`:  
  ![Environment Variables](img/04-Environment_Variables.png)
  5. Click on the "Ok" button and close all windows:  
  ![Edit Env. Variables](img/05-Edit_User_Variable.png)
5. Unzip the `eac3to327.zip` file into the directory:  
  ![Files](img/06-brdsoft.png)
6. Unzip the `SubExtractor1031.zip` file into the directory.
7. Unrar the `suprip-1.16.rar` file into the directory.
8. Unzip (7zip) `mkvtoolnix-amd64-6.8.0.7z` into directory:  
  ![Files](img/09-brdsoft.png)
9. Create a folder for your rip, in this guide I'll use: `C:\bdrip`:  
  ![Folder](img/10-folder.png)


### Demuxing
1. Check which drive letter identify your Blu-ray Disc, mine is `D:`:  
  ![Drive](img/11-drive.png)
2. Using your Command Prompt, go to your rip directory.  
  ![Dir](img/12-dir.png)
3. Type `eac3to D:` to list all playlist tracks on the disc:  
  ![Playlists](img/13-pls.png)
4. Now let's check the playlist information by typing `eac3to D: 2)`:  
  ![Playlists Info](img/14-plinfo.png)
5. Now let’s see which tracks to extract from the disc, you have to choose which fit your preference, typically you'll choose the chapters track, the main video track(s), the original audio track, the audio track that is on my native language, the original subtitles, the subtitles in my native language.
6. To extract my desired tracks I type the following command:  
  ```eac3to D: 2) 1:chap.txt 2:left.h264 3:right.h264 4:en.dts -core 7:es.ac3 9:en.sup 11:es.sup```  
  This command tells `eac3to` to extract (demux) form the `D:` drive, from the `2)` playlist, the `1:` track as a chapter file, the `2:` track as a left eye H264 video stream, the `3:` track as the right eye H264 stream (which is not an standard H264 stream but an *AVC Stereo* stream), the `4:` English audio track on DTS Core format (core means 5.1), the `7:` Spanish audio track on AC3/Dolby format, the `9:` English subtitles track, and finally the `11:` Spanish subtitles track:  
  ![Playlists Info](img/15-demux.png)
7. The extracted file tracks should look like this:  
  ![Demuxed Files](img/17-bdrip.png)


> **IMPORTANT**: Write down the length of the track and the frame rate, we will use this values later, in this guide the track length is `1:52:03` and the frame rate is `24p /1.001` (29.976).

> **Note on Video**: For this guide I'm using a 3D movie, there is nothing to worry about, the main difference between a 2D and a 3D is the extra video track for the right eye, if you don't want to create a 3D movie you can ignore the extraction of this track.

> **Note on Audio**: Most Home Theater Systems support Dolby Digital up to 5.1, [Apple TV 3](http://support.apple.com/kb/sp648), [Logitech Z-5500](http://reviews.cnet.com/pc-speakers/logitech-z-5500/4507-3179_7-31115626.html) and [Z906](http://www.logitech.com/en-us/product/speaker-system-z906) Speaker Systems doesn't support more than 5.1, that's why we are not using the 7.1 DTS audio track but the 5.1 core track, but is up to you to use DTS 7.1 instead.

### Video Encoding

#### For most Smart TVs and Apple TV

1. For encoding we will use *HandBrake*, but first we have to give *HandBrake* a video format that can understand, *HandBrake* can't encode a H.264 file directly, so we have to mux the file into an MKV container, open `mmg.exe` on the `C:\brdsoft\mkvtoolnix` folder.  
![mkvtoolnix](img/18-mkvtoolnix.png)
2. drag your `left.h264` track file into the *mkvmerge GUI* window:  
![mkvtoolnix](img/19-drag.png)
3. After dragging your track, *mkvmerge GUI* will automatically define an output file name for your video, just click on the "Start muxing" button and wait until it finishes:  
![mkvtoolnix muxing](img/20-dragged.png)
4. After muxing, click the *Ok* button and close *mkvmerge GUI*, then, open *HandBrake*, and drag the `left.mkv` we just created to the *HandBrake* window.
5. Because we want a very compatible file, we will select the `Apple TV 3` preset from the presets on the right. *HandBrake* automatically decide how to crop the video, this is useful but sometimes isn't accurate, I'll fix the crop option to keep the removal of the letterboxing but not the left and right pixels, and after that I'll make sure the video width is `1920`:  
![HandBrake Picture Tab](img/23-hb.png)
6. Now, knowing my video isn't interlaced, I'll disable any filter on the filter tab:  
![HandBrake Filter Tab](img/24-hb.png)
7. Knowing my video track run at `23.976fps` I'll set that value and select `Constant frame rate`, this is mainly because sometimes *HandBrake* doesn't know how to handle frame rates, then enable the `Fast decode` check box to make it friendly with more devices, and finally on `x264 Tune` set it to `Film`, you can choose a more convenient tune depending on your content, for animated movies "Animation" works best:  
![HandBrake Video Tab](img/25-hb.png)
8. **IMPORTANT**: Since we don't have any audio, subtitle or chapter included (we are only encoding the video track), let's disable any option on the tabs, also, **we will use MKV as our output format** so it can be remuxed later:  
![HandBrake Extra Tabs](img/26-hb.png)
9. Then press the *Start* button and wait for the encoding to finish.
10. After the video encoding is done, we do the [audio encoding](#audio-encoding).

#### 3D SBS Video Encoding

Side-by-side 3D encoding is something special, 3D Blu-ray Discs have two different video streams for each eye, so the encoding requires to merge the "right" and "left" video streams into one video, then squeeze both videos to fit the original video dimension, but there is something tricky, the "right" video stream isn't a typical H.264 stream but a *"Stereo H.264"*, so for that reason we need some extra software to decode it

We can't use *HandBreak* for video encoding because [it doesn't handle *AviSynth*](https://forum.handbrake.fr/viewtopic.php?f=23&t=21092#p97222) and because *HandBreak* doesn't have the availability to merge two videos into one video (compositing) so instead we use *X264* directly.

*AviSynth* is a [frameserver](http://en.wikipedia.org/wiki/Frameserver) script based, it can read, decode and serve the resulting video frames to any application that support frameservers (frame client), we use it to decode and merge the left and right video tracks, the kind of thing you can achieve with Premiere or Vegas, but free.

##### Software and Scripts Required for SBS Video Encoding

* [X264](http://www.videolan.org/developers/x264.html): For encoding - free,
  [Direct Download](http://download.videolan.org/pub/videolan/x264/binaries/win32/x264-r2409-d6b4e63.exe).
* [AviSynth](http://avisynth.nl/index.php/Main_Page): To merge both videos - free,
  [Direct Download](http://sourceforge.net/projects/avisynth2/files/latest/download).
* [ffdshow](http://www.videohelp.com/tools/ffdshow) - Required for H264 decoding/encoding - free,
  [Direct Download](http://www.videohelp.com/download/ffdshow_rev4530_20140209_clsid.exe).
* [MVC Decoder](http://www.fbx.ro/4cbzkmk91j46j3v3): To decode Stereo H264 - free,
  [Direct Download](https://mega.co.nz/#!mBVVyLYY!tpfVQWYmZjChLL3zmu5VaaPAODdAI-IVf2FSaTUCVjA).
* [Pantarheon 3D AviSynth Toolbox](http://www.pantarheon.org/AviSynth3DToolbox/): To handle stereoscopic *AviSynth* functions - free,
  [Direct Download](http://www.pantarheon.org/AviSynth3DToolbox/msi/).

##### System Preparation

* Install AviSynth.
* Install ffdshow.
* Install Pantarheon 3D AviSynth Toolbox.
* Download and unzip x264 for "win32" (this is important, don't use the X64 version because is incompatible with AviSynth).
* Rename the `x264-r2409-d6b4e63.exe` file to `x264.exe`
* Move the `x264.exe` file to the `c:\brdsoft` folder so x264 can be called wherever it is needed:  
![X264 on brdsoft folder](img/30-brdsoft.png)
* Download, unrar `H264StereoSource_a2.rar` **and put its contents into the `c:\brdsoft` folder**:  
![H264StereoSource](img/31-bdrip.png)


##### AviSynth Script configuration

> **VERY IMPORTANT**: Remember we write down the video length and frame rate? this is needed because the H.264 streams are raw video streams, we need to provide the length of the streams in frames so AviSynth can decode it, it requires simple math, our video track length is `1:52:03`, let's convert that into seconds:

```
01h = 60m
60m + 52m = 112m
112m * 60s = 6720s
6720s + 03s = 6723s
```

Now that we know the length in seconds, we have to calculate the total frames, this is quite easy, the movie has 23.976fps, that means that for each second of video there are `23.976` frames, but since that isn't an accurate number most times you have to use a simple formula that represent that number, it can be either `(24000/1001)` or `(24/1.001)`, so our final calculation is:

```
6720 * (24/1.001) = 161118
```

Now let's edit the `sample.avs` file in a text editor, the original file content is the following:

```
LoadPlugin("H264StereoSource.dll")
H264StereoSource("decoder.cfg",161214).AssumeFPS(24000,1001)
```

Change it so the final content looks the text above, change the total frames and the `AssumeFPS` function depending on your own video specs:

```
LoadPlugin("H264StereoSource.dll")
lv = directshowsource("left.mkv", audio=false)
rv = H264StereoSource("decoder.cfg",161118).AssumeFPS(24000,1001)
LeftRight3DReduced(lv, rv)
```

Here is what the final `sample.avs` script does line by line:

1. Load the `H264StereoSource.dll` plugin so it can read the "right" or "Stereo" video track.
2. Then it creates an instance of the "left" video track we muxed earlier in MKV format.
3. Then it creates an instance for the "right" video track based on the `decoder.cfg` file that reads both `left.h264` and `right.h264` video tracks to generate the "right" video.
4. Finally it uses a function from the *Pantarheon 3D AviSynth Toolbox* to fit both video tracks together and squeeze them into the same space.

> **IMPORTANT**: Notice we change the total frames number in the 3th line, this is the number we obtained in the previous calculation, in this case the result is the number `161118`.

Now we save and close the `sample.avs` file, let's start encoding the video.

##### Encoding

To encode video frames from the AviSynth `sample.avs` script we use x264, the following command uses almost the same configuration that *HandBrake* use for `Apple TV 3` encoding, type this command in the Command Prompt and press [ENTER] to start encoding:

```
x264 --thread-input --preset medium --profile high --level 4 --crf 20 --tune film --ref 3 --bframes 3 --b-pyramid normal --direct spatial --subme 7 --merange 16 --b-adapt 2 --partitions p8x8,b8x8,i4x4 --vbv-bufsize 31250 --vbv-maxrate 25000 --output sbs.h264 sample.avs
```

![x264.exe encoding](img/32-encoding.png)

> **Note**: The encoding task can take some time, this is because we are decoding both full HD video tracks, then we are merging both tracks together, then squeezing both tracks to have the same width as the original video, and then encoding the result, this is a CPU intensive task and in my case it took a total of 7 hours, 14 minutes and 15 seconds to finish.


When the encoding is done you will find the `sbs.h264` file in your encoding folder, this is the Side-by-side encoded video, now let's encode the audio.

![SBS Encoded File](img/33-result.png)

### Audio Encoding

This step is easy, but first let's understand why we have to encode the audio tracks, first is the compatibility factor, AC3/A52/Dolby is the most supported digital audio format out there, DTS is not, second, Apple TV can't handle DTS, and third and most important, recoding the audio save a lot of disk space.

The most common audio formats on Blu-ray Discs are DTS and Dolby, and the most common audio channel configurations are 5.1 and 7.1, eventually mono and 6.1 (Star Wars for example). `eac3to` is mainly an audio encoding tool and it really shines at that, we are going to encode audio with this tool, if you are a truly audio enthusiast and really want a *super-human-ear-quality-audio* you should check how to enable [superior quality decoders](http://en.wikibooks.org/wiki/Eac3to/How_to_Use#Audio_Decoders) into `eac3to`.

In this case we have two audio tracks, `en.dts` is the English DTS 5.1 audio track which was extracted from the "DTS-HD Master Audio 7.1" audio track, and `es.ac3` is the Dolby 5.1 Spanish audio track.

First let's encode the English audio on the Command Prompt using the following command:

```
eac3to en.dts en_encoded.ac3 -448
```

![DTS to AC3 480](img/34-audio.png)

This command tells `eac3to` to encode the `en.dts` track into a Dolby audio track `en_encoded.ac3` with 448Kbps audio quality, the quality you use is at your discretion but from my personal experience with many digital/optical audio speakers systems I can tell that there is not a significant perceptible difference in quality going beyond 448Kbps, but it is a significant hard drive space wasted, so the decision is up to you.

Now let's encode the "es.ac3" audio track on the command prompt with the following command:

```
eac3to es.ac3 es_encoded.ac3 -448
```

![AC3 640 to AC3 480](img/35-audio.png)

That's all with the audio encoding, the original English audio track uses 1.18GiB (1,268,183,720 bytes) and the reencoded audio uses only 359MiB (376,506,368 bytes), that is 3.36 times less (70.31%) than the original, same thing with the Spanish audio track, from 512 MiB (537,866,240 bytes) to 359MiB (376,508,160 bytes) 30% less.

> **Fun fact**: "eac3to" encode Dolby audio using "Aften", which is a free/open source library for Dolby encoding, the name "Aften" came from "A Fifty-Two ENcoder", Dolby is also known as a A52 audio format.

### Subtitles
Subtitles or captions are optional. The subtitles we extract from a Blu-ray Disc are a sequence of images, but most video players doesn't support them or work better with text subtitles, and text subtitles are way smaller than the originals. To "convert" the original subtitles we have to make an [OCR](http://en.wikipedia.org/wiki/Optical_character_recognition) of the original subtitles, for that task you can use either "SubExtractor" or "SupRip".

**SubExtractor** is fast and easy but sometimes the result isn't great, here is a video showing how to do the OCR:

VIDEO_SUBEXTRACTOR

**SupRip** is less fancy than SubExtractor, with a very simple interface, the OCR process takes longer than with SubExtractor but the results are better, here is a video showing how to do the OCR:

VIDEO_SUPRIP

> **IMPORTANT NOTE**: make sure to save your subtitles on UTF8 encoding, you can use any text editor to do exactly that, open your SRT file in your text editor (notepad for example) and then choose save the file choosing the UTF8 encoding on the "Save As" dialog.

![Notepad Save as](img/39-srt.png)

![Notepad Encoding](img/40-srt.png)

> *OPTIONAL STEP*: If you want to make sure your subtitles are in good shape, look for errors on them using [Subtitle Workshop 2.51](http://www.urusoft.net/downloads.php?lang=1), but BE AWARE that this program can only open ANSI encoded text, so before open your SRT file make sure to encode it as ANSI with any text editor, and when you are done, save it again on UTF8 with any text editor, if you want to avoid text encoding issues always use UTF8.

![Subtitle Workshop](img/41-subtitle.png)

### Remuxing
Now that we have the video and audio tracks encoded we join them together, this action is commonly known as muxing or remuxing, for that task we use *mkvmerge GUI*, open `mmg.exe` which is located on your `C:\brdsoft\mkvtoolnix` folder.

We haven't prepared our chapters track, first select **Chapter Editor** tab on the *mkvmerge GUI* window, then drag the `chap.txt` file into the tab.

![Subtitle Drag](img/44-drag.png)

Now is up to you naming your chapters as `Chapter 1`, `Chapter 2`, etc. You can also name them as the chapter name it has in the disc box (Some music concerts have chapter names) or leave it as is.

After naming your chapters save your chapter xml file by clicking on the "`Chapter Editor->Save as`" menu, I use the file name `chap.xml`.

![Subtitle Drag](img/46-ch.png)

#### Remux for most Smart TVs and preparing for Apple TV

This MKV file will include an arrangement of the tracks in the following order:

1. Video: `left-1.mkv` (the one encoded with HandBrake)
2. English Audio Track: `en_encoded.ac3`
3. Spanish Audio Track: `es_encoded.ac3`
4. English Subtitles: `en.srt`
5. Spanish Subtitles: `es.srt`

Now, select the **Input** tab on *mkvmerge GUI* window and drag one by one in order each file into the *mkvmerge GUI* window and then uncheck the **Global tags** track, it has to look like this:

![Mux List](img/48-mk.png)

Now let's specify some details on each track, set the language of the audio tracks and subtitle tracks:

![Audio Track Lang](img/49-mk.png)

![Subtitle Track Lang](img/50-mk.png)

Set the subtitle encoding to UTF8 on each subtitle track:

![Subtitle Encoding](img/51-mk.png)

Set the chapter track, click on the **Global** tag, on the **Chapters file** browse and select the XML chapter file we made before `chap.xml`:

![Chapters](img/52-mk.png)

> **IMPORTANT**: Set the output file name, it is highly recommended to name your file with the movie title as it appears on [IMDB](http://www.imdb.com), with the name of the movie and the year, in this way media player, media centers and other video software an lookup information about your movie on the internet, XBMC and iFlicks do it in that way, I'll name my file "*Thor - The Dark World (2013).mkv*".

Then click the **Start muxing** button:

![Muxing](img/53-mk.png)

And we are done, here are the final file specs:

```
Name.........: Thor - The Dark World (2013).mkv
Size.........: 3.80 GiB
Duration.....: 01:52:03.384
Resolution...: 1920x800
Codec........: AVC High@L4.0
Bitrate......: 3 858 Kbps
Framerate....: 23.976 fps
Aspect Ratio.: 2.40:1
Audio........: English 448 Kbps CBR 6 chnls AC3
Audio........: Spanish 448 Kbps CBR 6 chnls AC3
Subs.........: English, Spanish.
```

#### For Apple TV and modern iOS devices

To create a M4V file compatible with *Apple TV 3* and most modern iOS devices we process the MKV file we just created in [the previous step](#remux-for-most-smart-tvs-and-preparing-for-apple-tv) with the commercial app [iFlicks 2](http://itunes.apple.com/us/app/iflicks-2/id731062389), to avoid video re-encoding by this app always use `X264 High Profile, Level 4` when encoding video. In this guide I'll use the `Thor - The Dark World (2013).mkv` we just make in [the previous step](#remux-for-most-smart-tvs-and-preparing-for-apple-tv), check the following video on how to use iFlicks 2:

VIDEO_IFLICKS

*iFlicks 2* automatically create the stereo version of each Dolby audio track, it adds all the necessary metadata, cover, and remux the movie as a M4V video ready to be used on iTunes or any modern iOS device.

Here are the final *iFlicks 2* file specs:

```
Name.........: Thor - The Dark World (2013).m4v
Size.........: 4.07 GiB
Duration.....: 01:52:03.370
Resolution...: 1920x800
Codec........: AVC High@L4.0
Bitrate......: 3 953 Kbps
Framerate....: 23.976 fps
Aspect Ratio.: 2.40:1
Audio........: English 164 Kbps VBR 2 chnls AAC LC
Audio........: English 448 Kbps CBR 6 chnls AC3
Audio........: Spanish 164 Kbps VBR 2 chnls AAC LC
Audio........: Spanish 448 Kbps CBR 6 chnls AC3
Subs.........: English, Spanish.
```

#### MKV for Side-by-side 3D File

Let's open *mkvmerge GUI* again and repeat almost the same steps as in the [For most Smart TVs and preparing for Apple TV](#remux-for-most-smart-tvs-and-preparing-for-apple-tv) step with one small difference, **the video track**, so this MKV file will include an arrangement of the tracks in the following order:

1. Video: `sbs.h264` (the one encoded with X264 and AviSynth)
2. English Audio Track: `en_encoded.ac3`
3. Spanish Audio Track: `es_encoded.ac3`

So just as in the [For most Smart TVs and preparing for Apple TV](#remux-for-most-smart-tvs-and-preparing-for-apple-tv) step, set the language on all audio tracks, **DO NOT INCLUDE SUBTITLE TRACKS**, subtitle tracks don't work well on Side-by-side 3D because when the movie is shown it blends both sides of the video, so you will see the half subtitles on each eye, you can create a 3D subtitle with [3DSubtitler](http://www.videohelp.com/tools/3DSubtitler) and include them when muxing the video, but again, the result don’t work very well, this is mainly because when you are watching a 3D movie ([stereoscopic movie](http://en.wikipedia.org/wiki/Stereoscopy)) your eyes are focusing on the main subject on each scene, when you try to read the subtitles your focus point changes, this is very exhaustive to your eyes, I'll not recommend using subtitles but is up to you.


> **IMPORTANT**: Some media players can read the 3D information from the MKV file, 3D is in fact [Stereoscopy](http://en.wikipedia.org/wiki/Stereoscopy), so let's set this setting selecting the video track, clicking the *Format specific options* and then choosing *side by side (left first)* option.

![Muxing SBS](img/55-mk.png)

Then set the file name, in this case I will use the [Thor - The Dark World (2013) SBD-3D.mkv] file name so I'll know that it is a 3D movie, finally click the *Start muxing* button.

And we are done, here are the final file specs:

```
Name.........: Thor - The Dark World (2013) SBD-3D.mkv
Size.........: 3.78 GiB
Duration.....: 01:52:03.360
Resolution...: 1920x1080
Codec........: AVC High@L4.0
Bitrate......: 3 839 Kbps
Framerate....: 23.976 fps
Aspect Ratio.: 16:9
Audio........: English 448 Kbps CBR 6 chnls AC3
Audio........: Spanish 448 Kbps CBR 6 chnls AC3
```

## Results

On XBMC
![XBMC](img/61-XBMC.png)

On QuickTime OS X
![QuickTime Lang](img/59-QuickTime.png)
![QuickTime Chap](img/60-QuickTime.png)

On iTunes
![iTunes](img/58-iTunes.png)

On Windows and OS X
![OS X](img/57-end-mac.png)
![Windows](img/56-end-pc.png)

SBS On VLC Windows
![VLC](img/62-VLC.png)

SBS Interlaced on Stereoscopic Player Windows
![iOS](img/63-Stereoscopic-Player.png)

On iOS
![iOS](img/65-iPhone5_1.png)
![iOS](img/66-iPhone5_2.png)
![iOS](img/67-iPhone5_3.png)
![iOS](img/69-iPhone5_5.png)

