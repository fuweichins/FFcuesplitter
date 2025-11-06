# FFcuesplitter - FFmpeg-based audio splitter for CDDA images associated with .cue files .

[![Image](https://img.shields.io/static/v1?label=python&logo=python&message=3.9%20|%203.10%20|%203.11%20|%203.12&color=blue)](https://www.python.org/downloads/)
[![Python application](https://github.com/jeanslack/FFcuesplitter/actions/workflows/CI.yml/badge.svg)](https://github.com/jeanslack/FFcuesplitter/actions/workflows/CI.yml)

FFcuesplitter is a multi-platform CUE sheet splitter entirely based on FFmpeg.
Splits big audio tracks and automatically embeds tags using the information
contained in the associated **"CUE"** sheet. It supports multiple CUE sheet
encodings (via charset-normalizer) and many input formats (due to FFmpeg), including 
APE format, without need installing extra audio libs and packages. It has the ability 
to accept both files and directories as input while also working in recursive mode. It can 
be used either as a [Python module](https://github.com/jeanslack/FFcuesplitter#using-python) 
or from the [command line](https://github.com/jeanslack/FFcuesplitter#using-command-line).

## Features

- Supports many input formats, due to FFmpeg.
- Convert to WAV, FLAC, Ogg, Opus,  MP3, and M4A (containing AAC, ALAC codecs) formats.
- Ability to copy source codec and format without re-encoding.
- Batch mode processing is also available.
- Accepts both files and directories.
- Ability to perform recursive searches.
- Ability to generate audio collection directories (Artist/Album/TrackNumber - Title)
- Auto-tag from CUE file data.
- Features automatic character set detection for CUE files (via [python3-charset-normalizer](https://pypi.org/project/charset-normalizer/)).
- Ability to remove original file after conversion.
- Works on Linux, macOS, FreeBSD, Windows.
- It can be used either as a Python module or from the command line.

## Features (branch-specific)

+ Convert to ALAC/AAC code with M4A container format for iTunes/Apple Music
+ Support output M3U playlist
+ Simplified logging format, changed same album file name pattern as iTunes/Apple Music

## Requirements

- Python >=3.9
- FFmpeg 

## Install

Install dependencies

```sh
### To install Python
# [macOS] Install "Xcode Command Line Tools" which includes tools like Python, Git
xcode-select --install
# or install Python with Homebrew
brew install python

# [Windows] If you have Visual Studio installed, you may install optional Python Tools with Visual Studio Installer
# or install Python with Chocolatey
choco install python

# or manually download Python from https://www.python.org/downloads/
# ensure that ffmpeg bin folder is added to enviroment variable PATH

### To install FFmpeg
# [macOS] Install FFmpeg with Homebrew,
brew install ffmpeg
# [Windows] Install FFmpeg with Chocolatey
choco install ffmpeg

# or manually download FFmpeg from https://www.ffmpeg.org/download.html
# ensure that FFmpeg bin folder is added to enviroment variable PATH

```

Install this branch of FFcuesplitter 

```sh
# Checkout/Download repo fuweichins/FFcuesplitter to ~/Documents/GitHub/
# with git command line
cd ~/Documents/GitHub/
git clone https://github.com/fuweichins/FFcuesplitter
# or with GitHub Desktop app

# Install local python package
pip3 install ~/Documents/GitHub/FFcuesplitter/
```

Note: You may need to add python bin path ( e.g. "~/Library/Python/3.9/bin/") to enviroment variable PATH in order to directly use command `ffcuesplitter`. 

## Usage

```
ffcuesplitter -i FILENAMES DIRNAMES [FILENAMES DIRNAMES ...]
              [-r]
              [-f {wav,flac,mp3,ogg,opus,alac,aac}]
              [-o OUTPUTDIR]
              [-del]
              [-c {author+album,author,album}]
              [-ow {ask,never,always}]
              [-ce CHARACTERS_ENCODING]
              [--ffmpeg-cmd URL]
              [--ffmpeg-loglevel {error,warning,info,verbose,debug}]
              [--ffmpeg-add-params='parameters']
              [-p {tqdm,standard}]
              [--ffprobe-cmd URL]
              [--dry]
              [--prg-loglevel {error,warning,info,debug}]
              [-h]
              [--version]
```

**Examples**

To split and convert to `flac` format (default), and save them in current working directory

```sh
ffcuesplitter -i 'my-album.cue'
```

To split and convert to `alac` codec (with m4a container format) and save them in the `my-album-tracks` directory.

```sh
ffcuesplitter -i 'my-album.cue' -f alac -o 'my-album'
```

To splits the individual audio tracks into `aac` codec (with m4a container format)  and set bitrate of 192kbps

```sh
ffcuesplitter -i 'my-album.cue' -f aac -o 'my-album(aac)' --ffmpeg-add-params='-b:a 192k'
```

Notes: when running on macOS, VideoToolbox ALAC/AAC encoders "alac_at"/"aac_at" take prejudice over universal encoders "alac"/"aac".

**For further information and other examples visit the [wiki page](https://github.com/jeanslack/FFcuesplitter/wiki)**

***

## Using Python

```python
>>> from ffcuesplitter.cuesplitter import FFCueSplitter
>>> getdata = FFCueSplitter(**kwargs)
>>> tracks = getdata.audiotracks  # get all tracks data
>>> getdata.commandargs(tracks)  # get FFmpeg command/arguments recipes.
```
#### Getting additionals data

```python
>>> getdata.probedata  # ffprobe data of the sources audio files.
>>> getdata.cue.meta.data  # get CD info.
```

**For further information and other examples visit the [wiki page](https://github.com/jeanslack/FFcuesplitter/wiki)**

## License and Copyright

Copyleft: (C) 2025 Gianluca Pernigotto
Author and Developer: Gianluca Pernigotto
Mail: <jeanlucperni@gmail.com>
License: GPL3 (see LICENSE file in the source directory)
