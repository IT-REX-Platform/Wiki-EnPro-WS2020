todo

- do we keep the original?
- do we process at all?
	- if not, inspect file header when upload starts and possible reject unsupported formats immediately

---

# Video Processing

Since we're planning on building a video streaming feature that users are going to access through their web browser, we'll have to look into video formats and codecs as not all of them are supported by popular browsers.  
[This link](https://developer.mozilla.org/en-US/docs/Web/Media/Formats/Containers) takes you to a page on media container formats (file types). [Here](https://developer.mozilla.org/en-US/docs/Web/Media/Formats/Video_codecs) is an overview of the video formats most commonly used on the web.  
It seems as though Ilias' OpenCast Plugin works with **MP4/AVC (h.264)** files, which is one of the most common formats you will encounter on the internet. In layman's terms, when choosing a codec, you're deciding on a tradeoff between file size and processing overhead (and workload). There are additional factors you might want to take into consideration, but for our use case, these two are the most important.  
If we choose to go with a more modern codec, chances are we may be able to produce smaller files without sacrificing any visual quality, but processing will be more difficult, take more time and the end result may be less compatible with hardware and software out there. Keep in mind, the videos will have to be encoded when they are uploaded to our platform, introducing varying degrees of processing overhead–and when a user ultimately tries to access and watch them, their setup will have to decode the file during playback, which can be more or less straining depending on the codec used. For very modern codecs for example, the users' hardware may not be equipped with a hardware decoder thus forcing the setup to use a software decoder instead. This will typically consume more energy, drain batteries faster and thus emit more heat. In exchange, more efficient compression helps save disk space and transmission bandwidth (especially on our end, which can be beneficial going forward...).  
YouTube, being one of if not the most popular video streaming platform on the internet, uses **VP9** for most of their video quality brackets (and is working on transitioning to even more efficient ones as we speak). **VP9** is an open and royalty-free alternative to **HEVC (h.265)**, the successor to **AVC (h.264)**. For comparison, **h.265** can save up to 50% in raw file size compared to **h.264** without any perceivable loss in quality. **VP9** produces similar file sizes, but encoders are a little slower than the **h.265** ones.


## Check Video Container / Codecs Client-Side

I could't find a library which works on iOS/Android an web simultaneously.
For web we could use [mp4box.js](https://medium.com/@JackPu/how-js-get-video-codec-548a33cf7454) and for iOS/Android React-native-video](https://github.com/react-native-video/react-native-video).

 If we play the video in the app before we upload it, we can use the onLoad callback of react-native-video to display the codecs [onLoad](https://www.npmjs.com/package/react-native-video#onload).


## Additional Links
[Android supported formats](https://developer.android.com/guide/topics/media/media-formats.html)