# fwf: FFmpeg video editor
**If you are a consumer considering using this software, don't.** This was an experiment and important features don't work or are missing. [Olive](https://www.olivevideoeditor.org/) is an open source video editor that you may be interested in. Read the *Inherent problems* section for more information.


![main screenshot](https://i.imgur.com/ZKp3CaW.png)

Video editing software in JavaScript, made with Electron, on top of FFmpeg using [fluent-ffmpeg](https://github.com/fluent-ffmpeg/node-fluent-ffmpeg). Provides a simple GUI for editing videos with FFmpeg with a timeline, preview, and filter editor.

Architecture:
- Fluent-ffmpeg in the main process, starting ffmpeg processes as needed.
- GUI in the renderer process, stores all of the information and only sends render instructions to main over IPC.
- Express HTTP server in main process for streaming preview video.

### Filter editor
![filter editor screenshot](https://imgur.com/G2tLNam.png)

JSON editor GUI using [jsoneditor](https://github.com/josdejong/jsoneditor/), with presets. This lets you edit the filters that are passed to fluent-ffmpeg, which then turns them into FFmpeg options. This means you can use **any** video filter the FFmpeg binary supports.

### Inherent problems
This was an experiment to see if a consumer grade video editor is possible to make with HTML and JavaScript. I would say it is possible, the result just isn't very good. It's also obviously not pure JavaScript, since it uses FFMpeg as a backend. Problems:

1. Previews are slow, unreliable and limited, because the preview is rendered in FFMpeg and streamed through an internal server to the renderer. I also haven't been able to implement the streams feature, which would make it capable of rendering multiple clips chained together for the preview.
2. FFMpeg wasn't designed for a consumer grade video editing app.  HTML & JavaScript weren't designed for making desktop apps.
3. The FFMpeg binary has to be bundled with the app for easier installation, and this means using a custom build configuration. Into this custom configuration I haven't been able to integrate the Vue compilation that would be necessary to make the interface entirely Vue-based.

If you would like to use it anyway, you're free to do so. If you would like to help out with the development, PRs are greatly appreciated.

### License
Released under the MIT license, see LICENSE.

![splash](https://imgur.com/eYh7yqY.png)
