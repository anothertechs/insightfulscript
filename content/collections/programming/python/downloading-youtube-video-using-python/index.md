---
title: Downloading YouTube videos using Python
published: true
Tags: ["programming","python"]
date: 2021-06-19
description: "Downloading youtube video using python. Here we will be using pytube module for downaloding youtube videos.pytube is a lightweight, Pythonic, dependency-free, library for downloading YouTube Videos."
image: /images/youtube-python-download.webp
keywords: python,youtube,downloading,downaloder,pytube,tutorial,video,audio,example,downaloder,bot
---

# Tutorial- Downloading YouTube videos using Python

## Requirements

1. **Python (Obvious)**
2. **[pytube](https://pytube.io/en/latest/)**

### Installing

```bash
	pip install pytube
```

## Downloading Youtube video

After installing pytube, return to the text editor, open the Python file and import pytube:

```py
from pytube import YouTube
```

Copy the URL of the youtube video you want to downalod. Create instance of it in the next line of python code:

```py
url = 'https://www.youtube.com/watch?v=example'
video = YouTube(URL)
```

The pytube module works by giving you different streaming options. However, the video has a different stream resolution. So pytube allows you to download videos based on these.

For printing different stream from YouTube object write down following code:

```py
def print_stream(video):
		print(video.streams)

print_stream(video)

```

OUTPUT:

```bash
[<Stream: itag="18" mime_type="video/mp4" res="360p" fps="25fps" vcodec="avc1.42001E" acodec="mp4a.40.2" progressive="True" type="video">, <Stream: itag="22" mime_type="video/mp4" res="720p" fps="25fps" vcodec="avc1.64001F" acodec="mp4a.40.2" progressive="True" type="video">, <Stream: itag="137" mime_type="video/mp4" res="1080p" fps="25fps" vcodec="avc1.640028" progressive="False" type="video">, <Stream: itag="248" mime_type="video/webm" res="1080p" fps="25fps" vcodec="vp9" progressive="False" type="video">, <Stream: itag="136" mime_type="video/mp4" res="720p" fps="25fps" vcodec="avc1.4d401f" progressive="False" type="video">, <Stream: itag="247" mime_type="video/webm" res="720p" fps="25fps" vcodec="vp9" progressive="False" type="video">, <Stream: itag="135" mime_type="video/mp4" res="480p" fps="25fps" vcodec="avc1.4d401e" progressive="False" type="video">, <Stream: itag="244" mime_type="video/webm" res="480p" fps="25fps" vcodec="vp9" progressive="False" type="video">, <Stream: itag="134" mime_type="video/mp4" res="360p" fps="25fps" vcodec="avc1.4d401e" progressive="False" type="video">, <Stream: itag="243" mime_type="video/webm" res="360p" fps="25fps" vcodec="vp9" progressive="False" type="video">, <Stream: itag="133" mime_type="video/mp4" res="240p" fps="25fps" vcodec="avc1.4d4015" progressive="False" type="video">, <Stream: itag="242" mime_type="video/webm" res="240p" fps="25fps" vcodec="vp9" progressive="False" type="video">, <Stream: itag="160" mime_type="video/mp4" res="144p" fps="25fps" vcodec="avc1.4d400c" progressive="False" type="video">, <Stream: itag="278" mime_type="video/webm" res="144p" fps="25fps" vcodec="vp9" progressive="False" type="video">, <Stream: itag="140" mime_type="audio/mp4" abr="128kbps" acodec="mp4a.40.2" progressive="False" type="audio">, <Stream: itag="249" mime_type="audio/webm" abr="50kbps" acodec="opus" progressive="False" type="audio">, <Stream: itag="250" mime_type="audio/webm" abr="70kbps" acodec="opus" progressive="False" type="audio">, <Stream: itag="251" mime_type="audio/webm" abr="160kbps" acodec="opus" progressive="False" type="audio">]

```

From ouput of different stream choose the extension you want, then write down the following code to get the strem of that **extension**.

```py
ext_video = video.streams.filter(file_extension='your_extension')
print(ext_video)
```

OUTPUT:

```bash
[<Stream: itag="248" mime_type="video/webm" res="1080p" fps="25fps" vcodec="vp9" progressive="False" type="video">, <Stream: itag="247" mime_type="video/webm" res="720p" fps="25fps" vcodec="vp9" progressive="False" type="video">, <Stream: itag="244" mime_type="video/webm" res="480p" fps="25fps" vcodec="vp9" progressive="False" type="video">, <Stream: itag="243" mime_type="video/webm" res="360p" fps="25fps" vcodec="vp9" progressive="False" type="video">, <Stream: itag="242" mime_type="video/webm" res="240p" fps="25fps" vcodec="vp9" progressive="False" type="video">, <Stream: itag="278" mime_type="video/webm" res="144p" fps="25fps" vcodec="vp9" progressive="False" type="video">, <Stream: itag="249" mime_type="audio/webm" abr="50kbps" acodec="opus" progressive="False" type="audio">, <Stream: itag="250" mime_type="audio/webm" abr="70kbps" acodec="opus" progressive="False" type="audio">, <Stream: itag="251" mime_type="audio/webm" abr="160kbps" acodec="opus" progressive="False" type="audio">]
```

However, the module returns different streaming resolutions, starting with 360p at 720p and 1080p (possibly more). But when you look closely, every resolution has an itag value.

For example, itag = "22" for res = "720", and itag for 360p resolution is 18.

You can use this itag value to call the stream, including the `get_by_itag ()` function:

```py
def get_video_by_itag(ext_video,itag_num):
	return ext_video.get_by_itag(itag_num)

video_stream = get_video_by_itag(ext_video,your_tab_num_here)
```

Now, all you need is to downlaod video using `downlaod` method:

```py
def downlaod_stream(stream,file_name,path):
	stream.downlaod(filename = file_name,output_path=path)

downlaod_stream(video_stream,"First Youtube video","./")

```

Here the `output_path` is your prefferd downlaod directory.

Altogether your code will look something like this:

```py
#youtube video downaloder code

from pytube import YouTube

def print_stream(video):
		print(video.streams)

def get_video_by_itag(ext_video,itag_num):
	return ext_video.get_by_itag(itag_num)

def download_stream(stream,file_name,path):
	stream.download(filename = file_name,output_path=path)

if __name__ == '__main__':
	url = 'https://www.youtube.com/watch?v=example'
	video = YouTube(URL)
	print_stream(video)
	ext_video = video.streams.filter(file_extension='your_extension')
	print(ext_video)
	video_stream = get_video_by_itag(ext_video,your_tab_num_here)
	download_stream(video_stream,"First Youtube video","./")

```
