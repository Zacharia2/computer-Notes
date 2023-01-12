# FFmpeg 

"FFmpeg"这个单词中的"FF"指的是"Fast Forward"

## 一、概念

**容器(Container)**：容器就是一种文件格式，比如flv，mkv等。包含下面5种流以及文件头信息。

**流(Stream)**：是一种视频数据信息的传输方式，5种流：音频，视频，字幕，附件，数据。

**帧(Frame)**：帧代表一幅静止的图像，分为I帧，P帧，B帧。

**编解码器(Codec)**：是对视频进行压缩或者解压缩，CODEC =COde （编码） +DECode（解码）

**复用/解复用(mux/demux)**：把不同的流按照某种容器的规则放入容器，这种行为叫做复用（mux），把不同的流从某种容器中解析出来，这种行为叫做解复用(demux)。

**视频尺寸：** 指的就是视频的分辨率，常见的分辨率有4096*2304,1920*1080,720*576等。

**视频编码：** 视频编码方式就是指通过特定的压缩技术，将某个视频格式的文件转换成另一种视频格式文件的方式。视频编码格式常见到的有：MPEG-2 TS、Divx、Xvid、H.264、WMV-HD和VC-1。

**音频编码：** 音频编码方式指通过特定的压缩技术对音频数据进行处理的方法。

**帧率：** 帧率（即视频更新率）是用于测量显示帧数的量度。测量单位为“每秒显示帧数”（Frame Per  Second，FPS，帧率）或“赫兹”，单位用FPS用来描述视频每秒播放多少帧，而单位用赫兹用来描述显示器的画面每秒更新多少次。  一般帧率越高，视频画面越流畅。

**比特率：** 指每秒传送的比特(bit)数，即每秒传输的文件大小。比特率规定使用“比特每秒”（**bit/s** 或 **bps**）为单位。比特率越高，每秒传送的数据越大。

**采样率：** 采样率的单位是Hz，表示每秒采样的次数。单位时间内取样率越大，精度就越高，处理过的视频文件就越接近没有处理过的视频文件。

**码率：** 码率就是数据传输时单位时间传送的数据位数,一般我们用的单位是kbps即千位每秒。码率与体积成正比：码率越大，体积越大；码率越小，体积越小。由于文件体积与取样率是成正比的，所以几乎所有的编码格式都想用最低的码率达到最少的失真，“码率”就是失真度，码率越高越清晰，反之则画面粗糙而且马赛克多。

**视频位深度：** 用于指定图像中的每个像素可以使用的颜色信息数量，用“位即bit”为单位。

**音频位深度：** 单个声道的采样数据大小





## 二、媒体流

语法：-map file_number\[:stream_type][:stream_number]

这有一些特别流符号的说明：

1. -map 0 选择第一个文件的所有流

2. -map i:v 从文件序号i(index)中获取所有视频流，

   -map i:a 获取所有音频流，

   -map i:s 获取所有字幕流等等。

3. 特殊参数-an,-vn,-sn分别排除所有的音频，视频，字幕流

```sh
ffmpeg -i audio.m4s -i video.m4s -c copy -f matroska video.mkv

ffmpeg -i https://example.com/video.m3u8 -c:v hevc -c:a aac -f matroska video.mkv
```








## 常用格式和固定转换命令

**mkv 是一个非常好的封装格式。aac是一个非常好的音频编码格式，hevc（h265）是一个非常好的视频编码格式**

**无损音频编码格式用flac，电纸书通用格式用epub，aac格式是MP3格式的下一代也是最好的有损压缩格式**

Matroska媒体定义了三种类型的文件：MKV是视频文件，它里面可能还包含有音频和字幕；MKA是单一的音频文件，但可能有多条及多种类型的音轨；MKS是字幕文件。这三种文件以MKV最为常见。 

MKV最大的特点就是能容纳多种不同类型编码的视频、音频及字幕流，甚至连非常封闭的RealMedia及QuickTime这类流媒体也被它囊括进去，可以说是对传统媒体格式的一次大颠覆，几乎变成了一个万能的媒体容器。

hevc（h265）：-c:v libx265 -c:v hevc
aac: -c:a aac
MKV： -f matroska

```sh
ffmpeg -i input.ts -c:v libx265 -c:a aac -f matroska out.mkv
```








### Ffmpeg使用语法

```sh
ffmpeg [options] [[infile options] -i infile]... {[outfile options] outfile}...

-i	设置输入文件

-f	设置输出格式

-c	指定输出文件的编码

-vcodec( -c:v )	指定视频文件的编码默认为源文件编码

-acodec ( -c:a ) 	指定音频文件的编码默认为源文件编码

-r fps	设置帧率值，默认为25fps

-b bitrate	设置比特率，默认200kb/s

-bt tolerance 设置视频码率容忍度kbit/s
-maxrate bitrate设置最大视频码率容忍度
-minrate bitreate 设置最小视频码率容忍度
-bufsize size 设置码率控制缓冲区大小

-fix_sub_duration 

-y :覆盖同名的输出文件 

-i  ：资源文件

-vf：一般用于设置视频的过滤器 set video filters

subtitles= ：后面跟字幕文件，可以是srt，ass的

最后面的为目标文件。
-preset 设置一些编码参数，有很多level

    ultrafast
    superfast
    veryfast
    faster
    fast
    medium – default preset
    slow
    slower
    veryslow
    placebo（一般不用）

可以省略，默认是"medium",越慢质量越高

-qp 设置固定的量化参数 

 
```




### CBR设置：

  CBR设置一般用作直播流，比如视频会议。为输出设置CBR,有三个参数必须设置为同一个值。
  bitrate(-b option), minimal rate(-minrate), maximal rate(-maxrate)。

  maximal rate需要设置-bufsize选项。例如设置CBR为0.5Mbit/s。

>  ffmpeg -i in.avi -b 0.5M -minrate 0.5M -maxrate 0.5M -bufsize 1M output.mkv




### strict 跟标准的严格性

 ‘strict, f_strict integer (*input/output*)’

 Specify how strictly to follow the standards. `f_strict` is deprecated and should be used only via the `ffmpeg` tool.

 Possible values:

 1. ‘very’

   严格遵守规范或参考软件的较旧、更严格的版本

 2. ‘strict’

   严格遵守规范中的所有内容，无论后果如何

 - ‘normal’

 - ‘unofficial’

   allow unofficial extensions

   允许非官方延期

 - ‘experimental’

  允许使用非标准化的实验设备、实验(未完成/正在进行的工作/测试不充分)解码器和编码器。注意：实验解码器可能会带来安全风险，请勿将其用于解码不可信的输入。

ffmpeg -f concat -safe 0 -i filelist.txt -c copy output.mp4

filelist.txt
   		 file '绝对路径'



### 写入字幕

  由于mp4容器，不像MKV等容器有自己的字幕流。

  像MKV这种容器的视频格式中，会带有一个字幕流，可以在播放中，控制字幕的显示与切换，也可以通过工具或命令，将字幕从视频中分离出来。

  而MP4格式的容器，是不带字幕流的。所以如果要将字幕集中进去，就需要将字幕文件烧进视频中去。烧进去的视频，不能再分离出来，也不能控制字幕的显示与否。

  命令如下：

  ffmpeg -y -i 6e28.flv -vf subtitles=subscript.srt tt.mp4
  
  

### 压缩视频

  ffmpeg -i input.mp4 -c:v libx264 -crf 28 -preset veryfast -c:a copy -movflags +faststart output.mp4 -y
   这个命令压缩到400kbps码率，1280\*720的网上观看足够，DV视频用这个压缩到了1/15大小，很好用。