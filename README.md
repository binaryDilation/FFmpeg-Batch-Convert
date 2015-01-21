# FFmpeg-Batch-Convert
A program to batch convert video and audio files using FFmpeg.

What it does:
Searches for video files by extension (recursively, checks for streams to convert, if present it converts the files, appends the filename with "FFmpeg-Batch-Convert", then moves the old files to a directory named "CLEANUP".

How to use it:
1. Specify the directory to search for video files in Module 1, this is roughly Line 685 as of the commit when this was written.
2. Non-Recursive or recursive search?  The default is recursive search.  To switch to recursive uncomment Module 3a and comment out Module 3b.
3. By default, the script searches for the following file types for conversion: ".mp4", ".mkv", ".avi", ".mpg".  To add more files types add this inside of the parentheses:  "-o -iname \*.webm ".
4. By default, the script searches for H264 video and AAC audio.  If both are found in a file, the script does no processing moves on to examine the next file.  If neither or only one of those streams is not found, the script converts to H264/AAC as neccesary and passes through the correct stream inside of the .mp4 container.  For exmaple, if a file contains .mkv container
5. 
