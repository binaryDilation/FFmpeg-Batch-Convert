# FFmpeg-Batch-Convert
An FFMpeg bash script to batch convert video and audio files.

What it does:
Searches a directory/sub-directories for video files by file extension, checks the file for  audio & video streams (by codec) to convert, as necessary converts the streams to the desired codec, outputs into the desired container, appends the filename with "FFmpeg-Batch-Convert", then moves the old files to a directory named "CLEANUP".

How to use it:
Note:  All line numbers are of the Commit when this was written.

1. Specify the directory to search for video files in Module 2, this is roughly Line 694.

2. Non-Recursive or recursive search?  The default is recursive search.  To switch to non-recursive uncomment Module 4a and comment-out Module 4b.

3. By default, the script searches for the following file extensions for conversion: ".mp4", ".mkv", ".avi", ".mpg".  To add more file extensions add this inside of the parentheses at Line 702:  "-o -iname \*.webm ".

4. By default, the script searches for H264 video and AAC audio streams.  If both streams are found in a file, the script does no conversion and moves on to check the next file.  If only one or none of those streams is not found, the script converts to H264/AAC as necessary, passing through the correct stream, when available, into an .mp4 container.  For example, if a file is .mkv container/H264/mp3, the script will pass-through the H264 video stream, convert the mp3 audio stream to an AAC strems, and place both streams inside an .mp4 container.  The combination of .mp4/H264/AAC has the broadest support across platforms.  H264/AAC in the .mp4 container works on Android/GTV/Chrome/IE(Desktop/Mobile)/Safari, mostly in Firefox (w/ dependencies from the Operating System), but does NOT work in Chromium or Opera.  For more compatibility look here: https://developer.mozilla.org/en-US/docs/Web/HTML/Supported_media_formats
5. To search for a different stream besides H264 or AAC, replace that stream in the script with desired codec using the proper name FFMpeg uses.  These are the && If comparisons at Lines 706, 708, 720, and 732.  From the CLI:  "ffmpeg -codecs" is a good start to find out the correct names for codecs or consult the FFMpeg documentation.  If a new output codec is desired (which it almost always would be), edit the FFmpeg command described directly below in 6.
6.

describe default video and audio settings here.  continue explanation
