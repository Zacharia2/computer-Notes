由于mp4容器，不像MKV等容器有自己的字幕流。

像MKV这种容器的视频格式中，会带有一个字幕流，可以在播放中，控制字幕的显示与切换，也可以通过工具或命令，将字幕从视频中分离出来。

而MP4格式的容器，是不带字幕流的。所以如果要将字幕集中进去，就需要将字幕文件烧进视频中去。烧进去的视频，不能再分离出来，也不能控制字幕的显示与否。

命令如下：
```sh
ffmpeg -y -i 6e28.flv -vf subtitles=subscript.srt tt.mp4
```
命令解释：

-y :覆盖同名的输出文件

-i  ：资源文件

-vf：一般用于设置视频的过滤器 set video filters

subtitles= ：后面跟字幕文件，可以是srt，ass的

最后面的为目标文件。

————————————————

版权声明：本文为CSDN博主「ufocode」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。

原文链接：https://blog.csdn.net/ufocode/java/article/details/75475539