# X-Cut: Edit Videos with Subtitles

[English](README.md) | [简体中文](README.zh.md)

> A subtitle-driven, cross-platform desktop video editing tool. Say goodbye to timeline dragging — select, edit, and export videos using text instead.

## 🎉 Completely Free

**Starting from X-Cut 2.0.0, all features are completely free!**

✅ Unlimited media import — no limits on project media count  
✅ Unlimited timelines — create as many timelines as you need  
✅ Professional export — full support for FCPXMLD / FCP7 XML  
✅ AI speech recognition — built-in Whisper for auto subtitle generation  
✅ No ads, no subscription, no in-app purchases — purely free, dedicated to every creator  

## Introduction

The traditional video editing paradigm has dominated the industry for decades: import footage, drag it onto a timeline, make precise cuts, add transitions, and render the final output. This workflow is powerful and comprehensive, but for many content creators, it may be unnecessarily complex.

If you're a podcast editor who needs to trim an episode based on conversation content; if you're editing an interview video and want to quickly remove filler words like "um" and "uh" along with repetitive segments; or if you have a long video with subtitles and need to extract highlights based on the text — what you really need is not a full non-linear editing system, but a more intuitive way to select segments.

X-Cut was built for exactly these needs. Its core philosophy can be summed up in six words: **Edit videos with subtitles**.

## What is X-Cut

X-Cut is a cross-platform desktop application built with Electron, supporting both macOS and Windows. It uses subtitles as the core driving element for video editing, allowing users to complete video segment selection, editing, and exporting by reading and manipulating subtitle text.

Unlike traditional NLE software such as Premiere Pro, Final Cut Pro, or DaVinci Resolve, X-Cut has no complex timeline panels, no multi-track editing, and no transitions or effects. Instead, it turns subtitles into an interactive video segment selection interface — when you see a subtitle, you see the corresponding time range of the video; when you select a subtitle, you've selected a segment of video.

### Why Subtitles Can Edit Videos

This starts with the internal structure of video files.

A video file is wrapped in a **Container**, which encapsulates multiple **Tracks**: video track, audio track, and optional subtitle track. These tracks are synchronized through **Timestamps** — every frame of video, every segment of audio, and every line of subtitles knows exactly when it should appear.

Subtitle files (like SRT, VTT) are essentially **timestamp reference tables**:

```
1
00:00:01,000 --> 00:00:04,500
Hello everyone, welcome to this episode

2
00:00:04,800 --> 00:00:08,200
Today we're going to talk about an interesting topic
```

This means: subtitles are naturally an **index** for video. When you select a subtitle line, you're actually selecting the video and audio segment from `00:00:01.000` to `00:00:04.500`.

What X-Cut does is simple: **losslessly cut and recombine video based on subtitle timestamps**.

You don't need to manually mark in/out points, search for breaths in waveforms, or align frame by frame — subtitles have already done all this for you. You just need to read the text and decide what content is worth keeping.

### Why Subtitle-Based Editing is More Natural and Efficient

The essence of video is an information carrier. And subtitles are the smallest unit of information.

When you edit with subtitles:

- You see **content**, not waveforms
- You manipulate **semantics**, not timecodes
- You think about **story**, not technical parameters

For interview, podcast, course, and vlog videos where language is the primary information carrier, subtitle-based editing is 5-10x more efficient than traditional methods.

## Key Features

### Multi-Format Media Import

X-Cut supports importing a wide range of media file formats:

- **Video**: MP4, WebM, MOV, OGV, FLV, and more
- **Audio**: MP3, WAV, M4A, AAC, FLAC, and more
- **Images**: JPG, PNG, GIF, WebP, BMP, and more

Upon import, the application automatically retrieves media metadata (resolution, duration, frame rate) for subsequent editing and exporting.

### Subtitle-Driven Editing

This is X-Cut's core feature. After importing media, you can add subtitles in multiple ways:

- **Import External Subtitles**: Supports SRT, VTT, ASS/SSA, SUB, LRC, JSON, and other mainstream subtitle formats
- **Generate Blank Subtitles**: Automatically segments at intelligent durations, cutting at natural pauses
- **Whisper AI Speech Recognition**: Automatically generates timestamped subtitles for videos using an embedded Python environment and the OpenAI Whisper model
- **Smart Scene Detection**: Automatically detects scene change points in videos using the scenedetect library and generates corresponding subtitle segments

Once imported, the editor displays subtitles in a hierarchical structure: **Media → Subtitles → Segments → Entries**. Each subtitle entry corresponds to a time range in the video — hovering over it provides real-time preview of the corresponding video frame and audio.

### Quick Selection Operations

X-Cut provides a set of efficient selection operations within the subtitle editor:

| Action                 | Description                                                                  |
| ---------------------- | ---------------------------------------------------------------------------- |
| **Mouse Hover**  | Real-time preview of the video frame and audio corresponding to the subtitle |
| **Click**        | Select or deselect a subtitle entry                                          |
| **Click & Drag** | Batch-select subtitles as you drag across them                               |
| **Shift + Drag** | Batch-deselect subtitles as you drag across them                             |
| **Space Bar**    | Play/pause the current video                                                 |
| **B Key**        | Split a subtitle (based on time ratio)                                       |
| **D Key**        | Merge two subtitle entries on either side of a divider                       |
| **P Key**        | Capture the current frame to the desktop                                     |
| **I Key**        | Edit the current subtitle entry                                              |
| **U Key**        | AI re-recognize the current subtitle text                                    |
| **S Key**        | Split the current segment                                                    |

Selected subtitles are highlighted in orange for clear visual feedback.

### Timeline Management

X-Cut supports creating multiple timelines, each independently recording selected subtitle entries. You can organize different editing plans across timelines without interference. Timelines support drag-and-drop reordering, renaming, duplication, and deletion.

### Script Matching

Paste a script to automatically match subtitles and generate a timeline. Simply paste the script content into the editor, and X-Cut will automatically match the corresponding subtitle entries to quickly generate an editing timeline.

### Real-Time Preview & Playback

The right-side preview panel provides full media preview capabilities:

- Native playback of video, audio, and images
- Audio waveform visualization
- Time indicator showing the current preview position
- Timeline playback mode: plays all selected segments in sequence, with pause and seek support

The bottom timeline preview bar displays all selected segments as color blocks showing their proportions and text content. Clicking any block jumps directly to the corresponding segment.

### Video Export

After selecting segments, X-Cut uses FFmpeg for high-quality export:

- Segment-by-segment encoding followed by merging, ensuring precise time control
- Video: H.264 encoding, CRF 18, high-quality output
- Images: Automatically converted to video segments with silent audio
- Audio: Automatically combined with a video background and converted to standard video format
- Automatic handling of segments with different resolutions, with unified letterboxing
- Simultaneous export of VTT subtitle files
- Real-time export progress display

### Professional NLE Integration

- **FCPXMLD Export**: Seamless integration with Final Cut Pro, DaVinci Resolve, and Jianying
- **FCP7 XML Export**: Perfect compatibility with Adobe Premiere Pro

The exported files include correct media asset references, frame-aligned timecodes, and subtitle text embedded as Marker annotations.

## Technical Implementation

X-Cut's tech stack balances development efficiency and user experience:

| Layer                 | Technology                            |
| --------------------- | ------------------------------------- |
| Desktop Framework     | Electron 40                           |
| Build Tool            | Electron Forge + Vite                 |
| Frontend Framework    | React 19 + TypeScript                 |
| UI Components         | Ant Design 6 (localized)              |
| Drag & Drop           | @dnd-kit                              |
| Video Processing      | fluent-ffmpeg                         |
| AI Speech Recognition | OpenAI Whisper (embedded Python 3.12) |
| Scene Detection       | PySceneDetect (embedded Python 3.12)  |

Notably, X-Cut embeds a complete Python 3.12 runtime environment. On first launch, the application automatically extracts the Python runtime and FFmpeg tools to the user's directory and installs the Whisper and scenedetect dependencies via pip. The entire process is fully transparent to the user — no manual environment configuration is required.

### Three-Panel Layout

The project editing interface uses a classic three-panel layout:

- **Left Panel (Media Panel)**: Manages imported media files and subtitles. Both media and subtitle files support drag-and-drop reordering for flexible content arrangement, along with right-click context menu operations.
- **Center Panel (Editor)**: Displays the subtitle list on the left and the video preview on the right.
- **Right Panel (Timeline Panel)**: Manages the timeline list and handles video export.

All three panels can be resized by dragging the divider lines, and each can be toggled between hidden and visible.

## Use Cases

X-Cut is particularly well-suited for the following scenarios:

| Scenario                             | Description                                                              |
| ------------------------------------ | ------------------------------------------------------------------------ |
| **Podcast/Interview Editing**  | Remove filler words, pauses, and repetitive content for quick turnaround |
| **Tutorial/Course Production** | Delete recording mistakes, keep core knowledge points                    |
| **Meeting Recording Editing**  | Extract key speeches, generate highlight versions                        |
| **Vlog Rough Cut**             | Quickly screen footage, determine storylines                             |

If you frequently work with "talking head" videos, X-Cut will be an indispensable part of your workflow.

## Editions

**X-Cut 2.0.0 — Completely Free**

Starting from version 2.0.0, all features are completely free and open:

- Unlimited media — no more limits on the number of media items per project
- Unlimited timelines — create as many timelines as you need to organize your creativity
- FCPXMLD export — seamless integration with Final Cut Pro, DaVinci Resolve, and Jianying
- FCP7 XML export — perfect compatibility with Adobe Premiere Pro
- Script matching — paste a script to automatically match subtitles and generate a timeline

## How to Use

X-Cut's workflow consists of three steps:

**1. Import & Recognition**

- Drag and drop video files or folders to automatically import and match subtitles
- Or click the button to manually select content to import
- Use the built-in Whisper AI to automatically generate subtitles
- Or import existing SRT/VTT/ASS subtitle files

**2. Select & Delete**

- Browse the subtitle list and review content like reading a script
- Select the segments you want to keep (or delete the ones you don't)
- Supports batch selection, inverse selection, and segment operations

**3. Export & Integrate**

- One-click export of the edited video
- Or export FCPXML/FCP7 XML to continue refining in traditional editing software

Throughout the entire process, you hardly need to touch the timeline.

## Download

X-Cut project page: [https://thinking.vip/x-cut](https://thinking.vip/x-cut)

Available for macOS and Windows, with ZIP format installation packages.

---

*X-Cut v2.0.0 | Edit Videos with Subtitles*
