# 用 Homebrew 安裝 youtube-dl 下载 YouTube 影片

## 下载 youtube-dl

先安装Homebrew,打开终端输入以下命令下载：

```
brew install youtube-dl
```

## 安装ffmpeg

我们下载youtobe视频时可能用到嵌入字幕等功能，必须通过ffmpeg来实现。

```
brew install ffmpeg
```

## 下载影片

### 直接下载

先在终端CD到要下载的文件夹路径，然后执行如下命令

```
youtube-dl '视频链接'
eg:
youtube-dl https://www.youtube.com/watch?v=jNQXAC9IVRw
```

输入如上命令按Enter键即开始下载，默认下载最清晰视频。

### 批量下载

有时候我们需要一次性下载多个视频，这就需要使用列表方式进行下载了，比如说我就经常这样干

使用列表进行下载，依赖于 参数 -a。首先我们将需要下载的视频地址保存为一个文本，一行一个下载例子，类似于这样。

```
https://youtu.be/Oelwh8yv6h4
https://youtu.be/cHcD1LcmxfA
https://youtu.be/5KN0_-HgWNo
```

这里我假设保存视频的文件名为 test.txt，然后使用 参数-a 进行下载。

```
youtube-dl -a test.txt
```

使用列表下载有一个问题就是如果下载地址当中有一个视频地址是错误的话，youtube-dl 会直接退出。有时候我们需要下载的视频可能有几十个，其中难免会出错。这就需要使用 -i 忽略错误了。

类似于这样

```
youtube-dl -i -a test.txt
```

鉴于国内复杂的网络情况，有时候我们的目标站点可能无法访问，这就需要使用 --proxy 指定代理了，代理类型支持 HTTP HTTPS SOCKS5。

类似于这样

```
youtube-dl --proxy socks5://127.0.0.1:1080 -i -a test.txt
```

### 格式转换

默认下载的视频是WebM格式，电脑、手机一般使用mp4格式。因此，下载时需要加上参数 -f mp4指定视频格式。

```
youtube-dl https://www.youtube.com/watch?v=jNQXAC9IVRw -f mp4
```

-f后面的格式可以是3gp、aac、flv、m4a、mp3、mp4、ogg、wav、webm 等等

### 嵌入字幕

有时youtube影片会有不同的CC字幕可选择，我们可以通过youtube-dl将字幕嵌入影片中。

首先我们先列出可以下载的字幕，在youtube-dl下载指令后方加入`--list-subs`

```
youtube-dl https://www.youtube.com/watch?v=Qkf4farak1k --list-subs
```

youtube-dl分析youtube网页后，在最下方 Available subtitles列出可用字幕

```
zh-CN
en
zh
zh-TW
```

也就是简体中文、英文、中文、中文（台湾）

有嵌入字幕的youtube-dl指令：

- --write-sub 下载字幕
- --embed-sub嵌入字幕
- —-sub-lang zh-CN指定语言（简体中文）
- --all-subs下載所有字幕（如果要將所有可用的字幕嵌入）

如果我们要下载嵌入中文（台湾）的MP4格式视频，指令为：

```
youtube-dl https://www.youtube.com/watch?v=Qkf4farak1k --write-sub --embed-sub --sub-lang zh-TW -f mp4
```

支持嵌入字幕的视频格式包含：`mp4`、`mkv`、`webm`

### 指定下载位置
使用終端機，預設的目錄應該是「使用者資料夾」，因此若單純使用 youtube-dl 加影片網址的指令下載，應該會直接儲存到使用者資料夾中，這邊我們可以建立一個 youtube-dl 的設定檔，來設定預設的下載位置。一樣使用終端機，輸入：
```
mkdir -p ~/.config/youtube-dl

touch ~/.config/youtube-dl/config

vi ~/.config/youtube-dl.conf
```

接著按鍵盤 i 進入編輯模式，並貼上：

```
--output "/Users/使用者名稱/Downloads/%(title)s.%(ext)s"
```

請記得將使用者名稱替換成 macOS 使用者的目錄名稱。小撇步：可以先輸入 --output " 接著將「下載項目」或你想要的資料夾，拖曳到終端機中，帶入目錄路徑，再貼上 /%(title)s.%(ext)s" 結尾，就可以快速得到正確的路徑了。

接著按鍵盤 ESC 退出編輯模式，輸入 :x 再按 ENTER 儲存。

以上這段如果不太理解，可以先 Google 一下「vi 指令」學習一下這個編輯器怎麼使用。


## 参考

-  [youtube-dl 教程](https://niconiconi.fun/2019/05/27/youtube-dl-tutorial/)
-  [用 Homebrew 安裝 youtube-dl 下載 YouTube 影片](https://diary.taskinghouse.com/posts/download-youtube-videos-with-youtube-dl-install-by-homebrew/)
-  [youtube-dl，又一全网视频下载利器](https://zhuanlan.zhihu.com/p/48511222)


<video tabindex="-1" class="video-stream html5-main-video" controlslist="nodownload" style="width: 652px; height: 367px; left: 0px; top: 0px;" src="blob:https://www.youtube.com/795619bf-8f0b-4f5c-8cf1-b52f1f3ca05a"></video>