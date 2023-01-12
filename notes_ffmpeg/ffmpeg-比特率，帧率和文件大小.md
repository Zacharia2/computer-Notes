比特率和帧率是音视频基本的特性，对于音视频整体的质量有关键作用！如果知道比特率和持续时间，就可以计算输出文件的大小。

## Frame(frequency)rate introduction

帧率就是每秒编码进视频文件的帧数目。人类的眼睛需要每秒至少15帧才能将图像连贯在一起。帧率的单位是HZ，LCD显示一般有60Hz的平率。

有2种类型的帧率-interlaced(denoted asiafterFPSnumber) andprogressive(denoted aspafterFPSnumber)//逐行扫描和隔行扫描

逐行扫描(interlaced)的帧率一般用在电视：

-NTSC用60i fps，意思是：60 interlaced fields(30 frames)per second

-PAL and SECAM标准用50i fps，等于25帧每秒。

隔行扫描(progressive)帧率是24p，25p和30p，用在电影工业上。现在较新的帧率是50p/60p用在高档的HDTV产品上。

## 帧率设置

使用-r选项

语法是：

```sh
ffmpeg -iinput-r fpsoutput
```

例如：

```sh
ffmpeg -i input.avi -r 30 output.mp4
```

使用fps filter

另一个设置帧率是用fps filter，特别是在filterchains使用时非常有用

例如：修改输入文件的帧率到25

```sh
ffmpeg -v clip.mpg -vf fps=fps=25 clip.webm
```

对帧率预定义值

例如：设置帧率29.97fps

## 比特率设置

比特率也是一个决定音视频总体质量的参数。他决定每个时间单位处理的bit数。

设置比特率：

比特率决定处理1s的编码流需要多少bits，设置用-b选项。区分音视频用-b:a和-b:v

例如：设置整体1.5Mbit每秒

```sh
ffmpeg -i file.avi -b 1.5M file.mp4

ffmpeg -i input.avi -b:v 1500K output.mp4
```

CBR设置：

CBR设置一般用作直播流，比如视频会议。为输出设置CBR,有三个参数必须设置为同一个值。

bitrate(-b option), minimal rate(-minrate), maximal rate(-maxrate)。maximal rate需要设置-bufsize选项。例如设置CBR为0.5Mbit/s。

```
ffmpeg -i in.avi -b 0.5M -minrate 0.5M -maxrate 0.5M -bufsize 1M output.mkv
```
`
设置输出文件的最大size。

用-fs选项。

例如设置输出文件的最大的size为10M

```
ffmpeg -i input.avi -fs 10MB output.mp4
```

文件大小计算：

文件的大小是是音视频流大小的和。

视频流的大小的方程式是(除以8是由bits到bytes的转换):

```
video_size = video_bitrate * time_in_seconds / 8;
```

如果音频是解压缩的，计算公式是：

```
audio_size = smpaling_rate * bit_depth * channels * time_in_second / 8;
```

例如：计算10分钟的视频， 1500kbits/s 视频比特率和 128kbits/s的音频比特率，用下面的计算方法：
```
file_size = video_size + audio_size;

file_size = (video_bitrate + audio_bitrate) * time_in_seconds / 8;

file_size = (1500 kbits/s + 128kbits/s) * 600s

file_size = 1628kbits/s * 600s

file_size = 976800kb = 976800000 b / 8 = 122100000 B / 1024 = 119238.28125KB

file_size = 119238.28125 KB / 1024 = 116.443634033203125MB = 116.44M
```
From < [https://csdnimg.cn/release/phoenix/template/new_img/articleRead.png](https://csdnimg.cn/release/phoenix/template/new_img/articleRead.png)>