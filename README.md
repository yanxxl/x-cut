# X-Cut: Edit Videos with Subtitles

[English](README.md) | [简体中文](README.zh.md)

> A subtitle-driven, cross-platform desktop video editing tool. Say goodbye to timeline dragging — select, edit, and export videos using text instead.

## Introduction

The traditional video editing paradigm has dominated the industry for decades: import footage, drag it onto a timeline, make precise cuts, add transitions, and render the final output. This workflow is powerful and comprehensive, but for many content creators, it may be unnecessarily complex.

If you're a podcast editor who needs to trim an episode based on conversation content; if you're editing an interview video and want to quickly remove filler words like "um" and "uh" along with repetitive segments; or if you have a long video with subtitles and need to extract highlights based on the text — what you really need is not a full non-linear editing system, but a more intuitive way to select segments.

X-Cut was built for exactly these needs. Its core philosophy can be summed up in six words: **Edit videos with subtitles**.

## What is X-Cut

X-Cut is a cross-platform desktop application built with Electron, supporting both macOS and Windows. It uses subtitles as the core driving element for video editing, allowing users to complete video segment selection, editing, and exporting by reading and manipulating subtitle text.

Unlike traditional NLE software such as Premiere Pro, Final Cut Pro, or DaVinci Resolve, X-Cut has no complex timeline panels, no multi-track editing, and no transitions or effects. Instead, it turns subtitles into an interactive video segment selection interface — when you see a subtitle, you see the corresponding time range of the video; when you select a subtitle, you've selected a segment of video.

## Key Features

### Multi-Format Media Import

X-Cut supports importing a wide range of media file formats:

- **Video**: MP4, WebM, MOV, OGV, FLV, and more
- **Audio**: MP3, WAV, M4A, AAC, FLAC, and more
- **Images**: JPG, PNG, GIF, WebP, BMP, and more

Upon import, the application automatically retrieves media metadata (resolution, duration, frame rate) for subsequent editing and exporting.

### Subtitle-Driven Editing

This is X-Cut's core feature. After importing media, you can add subtitles in multiple ways:

- **Import External Subtitles**: Supports mainstream subtitle formats including SRT, VTT, ASS/SSA, and SUB
- **Generate Blank Subtitles**: Automatically creates segmented blank subtitle entries at fixed intervals (25 seconds)
- **Whisper AI Speech Recognition**: Automatically generates timestamped subtitles for videos using an embedded Python environment and the OpenAI Whisper model
- **Smart Scene Detection**: Automatically detects scene change points in videos using the scenedetect library and generates corresponding subtitle segments

Once imported, the editor displays subtitles in a hierarchical structure: **Media → Subtitles → Segments → Entries**. Each subtitle entry corresponds to a time range in the video — hovering over it provides real-time preview of the corresponding video frame and audio.

### Quick Selection Operations

X-Cut provides a set of efficient selection operations within the subtitle editor:

| Action | Description |
|--------|-------------|
| **Mouse Hover** | Real-time preview of the video frame and audio corresponding to the subtitle |
| **Click** | Select or deselect a subtitle entry |
| **Click & Drag** | Batch-select subtitles as you drag across them |
| **Shift + Drag** | Batch-deselect subtitles as you drag across them |
| **B Key** | Split a subtitle into two entries at the cursor position |
| **D Key** | Merge two subtitle entries on either side of a divider |
| **Space Bar** | Play/pause the current video |
| **P Key** | Capture the current frame to the desktop |

Selected subtitles are highlighted in orange for clear visual feedback.

### Timeline Management

X-Cut supports creating multiple timelines, each independently recording selected subtitle entries. You can organize different editing plans across timelines without interference. Timelines support drag-and-drop reordering, renaming, and deletion.

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

### FCPXMLD Export (Pro Version)

Pro users can export editing results in FCPXMLD format for direct import into Final Cut Pro for further editing. The exported file includes correct media asset references, frame-aligned timecodes, and subtitle text embedded as Marker annotations.

## Technical Implementation

X-Cut's tech stack balances development efficiency and user experience:

| Layer | Technology |
|-------|-----------|
| Desktop Framework | Electron 40.6 |
| Build Tool | Electron Forge + Vite |
| Frontend Framework | React 19 + TypeScript |
| UI Components | Ant Design 6 (localized) |
| Drag & Drop | @dnd-kit |
| Video Processing | fluent-ffmpeg |
| AI Speech Recognition | OpenAI Whisper (embedded Python 3.12) |
| Scene Detection | PySceneDetect (embedded Python 3.12) |

Notably, X-Cut embeds a complete Python 3.12 runtime environment. On first launch, the application automatically extracts the Python runtime and FFmpeg tools to the user's directory and installs the Whisper and scenedetect dependencies via pip. The entire process is fully transparent to the user — no manual environment configuration is required.

### Three-Panel Layout

The project editing interface uses a classic three-panel layout:

- **Left Panel (Media Panel)**: Manages imported media files and subtitles. Both media and subtitle files support drag-and-drop reordering for flexible content arrangement, along with right-click context menu operations.
- **Center Panel (Editor)**: Displays the subtitle list on the left and the video preview on the right.
- **Right Panel (Timeline Panel)**: Manages the timeline list and handles video export.

All three panels can be resized by dragging the divider lines, and each can be toggled between hidden and visible.

## Use Cases

X-Cut is particularly well-suited for the following scenarios:

1. **Podcast/Interview Editing**: Import subtitles generated from audio recordings and quickly locate and select highlight segments by reading the conversation text.
2. **Tutorial/Course Editing**: Quickly remove repetitive explanations, verbal mistakes, and invalid segments based on subtitle content.
3. **Meeting Recording Editing**: Use AI-generated subtitles to rapidly filter and select meaningful discussion content.
4. **Short-Form Content Curation**: Perform initial screening on long videos and export highlight clips for secondary creative work.
5. **Subtitle-Driven Workflows**: Any scenario where video editing decisions are guided by textual content.

## Editions

X-Cut is available in two editions:

**Free Edition** (permanently free):
- Create projects and import media (up to 3 items)
- Import/generate subtitles
- Timeline editing (up to 1 timeline) with real-time preview
- Video export

**Pro Edition** (activation code authorization, planned at $9.9/month, currently free):
- No limits on media items and timelines
- FCPXMLD export (for seamless integration with Final Cut Pro)
- More professional features coming soon

## Download

X-Cut project page: [https://thinking.vip/x-cut](https://thinking.vip/x-cut)

Available for macOS and Windows, with ZIP format installation packages.

---

*X-Cut v1.2.0 | Edit Videos with Subtitles*
