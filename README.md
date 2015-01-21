# FFmpeg-Batch-Convert
An FFMpeg bash script to batch convert video and audio files

What it does:
Searches for video files by extension (recursively, checks for streams to convert, if present it converts the files, appends the filename with "FFmpeg-Batch-Convert", then moves the old files to a directory named "CLEANUP".

How to use it:
1. Specify the directory to search for video files in Module 1, this is roughly Line 685 as of the commit when this was written.
2. Non-Recursive or recursive search?  The default is recursive search.  To switch to recursive uncomment Module 3a and comment out Module 3b.
3. By default, the script searches for the following file types for conversion: ".mp4", ".mkv", ".avi", ".mpg".  To add more files types add this inside of the parentheses:  "-o -iname \*.webm ".
4. By default, the script searches for H264 video and AAC audio.  If both are found in a file, the script does no processing moves on to examine the next file.  If neither or only one of those streams is not found, the script converts to H264/AAC as neccesary and passes through the correct stream inside of the .mp4 container.  For exmaple, if a file is .mkv container/H264/mp3, the script will pass through the H264 video stream, convert mp3 audio to AAC, and place both inside a .mp4 container.  The combination of .mp4/H264/AAC has the broadest support across platforms.  H264/AAC in .mp4 container works on Android/GTV/Chrome/IE(Desktop/Mobile)/Safari, mostly in Firefox (w/ dependencies from the Operating System), but does NOT work in Chromium or Opera.  For more compatbility look here: https://developer.mozilla.org/en-US/docs/Web/HTML/Supported_media_formats
5. If a person wants to search for different codecs besides H264 or AAC, replace that with one of the proepr name ffmpeg uses for the desired codec.  From the command line:  "ffmpeg -codecs" is a good start.
6. Additonally, the desired output codec will have to be changed in each of the ElseIf statements.

describe default video and audio settings here.  continue explanation
