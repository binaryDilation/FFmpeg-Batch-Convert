# FFmpeg-Batch-Convert
An FFMpeg bash script to batch convert video and audio files.

What it does:
Searches a directory/sub-directories for video files by file extension, checks the file for  audio & video streams (by codec) to convert, converts the streams to the desired codec as necessary, outputs into the desired container, appends the filename with `FFmpeg-Batch-Convert`, then moves the old files to a directory named `CLEANUP`.

How to use it:
Note:  All line numbers are of the Commit when this was written.

1. Specify the directory to search for video files in Module 2, this is roughly `Line 694`.

2. Non-Recursive or recursive search?  The default is recursive search.  To switch to non-recursive uncomment Module 4a and comment-out Module 4b.

3. By default, the script searches for the following file extensions for conversion: ".mp4", ".mkv", ".avi", ".mpg".  To add more file extensions add the extension inside of the parentheses at `Line 702`, e.g.: `-o -iname \*.webm `.

4. By default, the script searches for H264 video and AAC audio streams.  If both streams are found in a file, the script does no conversion and moves on to check the next file.  If only one or none of those streams is found, the script converts to H264/AAC as necessary, passing through the correct stream, when available, into an .mp4 container.  For example, if a file is .mkv container/H264/mp3, the script will pass-through the H264 video stream, convert the mp3 audio stream to an AAC stream, and place both video & audio streams inside an .mp4 container.  The combination of .mp4/H264/AAC has the broadest support across platforms.  H264/AAC in the .mp4 container works on Android/GTV/Chrome/IE(Desktop/Mobile)/Safari, mostly in Firefox (w/ dependencies from the Operating System), but does NOT work in Chromium or Opera.  For more compatibility look here: https://developer.mozilla.org/en-US/docs/Web/HTML/Supported_media_formats
5. To search for a different stream besides H264 or AAC, replace that stream in the script with desired codec using the proper name FFMpeg uses.  These are the `if &&` comparisons at `Lines 706, 708, 720, and 732`.  From the CLI:  `ffmpeg -codecs` is a good start to find out the correct names for codecs or consult the FFMpeg documentation.  If a new output codec is desired (which it almost always would be if the search codec is changed), edit the FFmpeg commands described directly below in
6.  The default FFMpeg options in order are;
`nice -19`        sets the processing priority to lowest possible.

`ffmpeg`          calls FFMpeg.

`-y`              overwrites output files.

`-probesize 100000000`        sets probing size in bytes, i.e. the size of the data to analyze to get stream information. A higher value will allow to detect more information and reduce errors.  This is twice the default.

`-analyzeduration 100000000`        specifies how many microseconds are analyzed to probe the input. A higher value will allow to detect more accurate information and reduce errors.  This is twice the default.

`-i "$FIL"`        specifies the input file by calling the variable for current file.

`-vcodec libx264`        specifies the h264 video codec (note:  this may have to be installed in your FFMpeg distribution).

`-crf 20`        specifies a constant quality of 20, which is a very good and will not be detected as different from loss-less from most viewers.  Specific to H264/H265 codecs.

`-preset veryslow`        very slow preset provides the highest compression and smallest file size, but at the slowest speed.  A preset is a collection of options that will provide a certain encoding speed to compression ratio. A slower preset will provide better compression (compression is quality per filesize).  This may be specific to the H264 codec and must be researched for use with other codecs.

`-acodec libfdk_aac`        specifies Fraunhofer FDK AAC audio codec  (note:  this may have to be installed in your FFMpeg distribution).

`-ac 2`        specifies 2-channel (i.e. stereo) audio.  This will downmix to 5.1 to stereo.  Remove this to preserve 5.1 audio steams.

`-b:a 128k`        specifies 128k bitrate, which for 2-channel (above) is 64k audio.  Most users won't be able to detect any difference from loss-less.  For more than 2-channel audio, simply multiply 64k by the number of channels e.g. 5.1 = 6 x 64 = 384k.  Or simply delete this and let FFmpeg sort it out.

`-cutoff 18000`        libfdk_aac defaults to a frequency cutoff of 14,000Hz, which is in the detectable range.  This raises it to 18,000Hz, near the limit of high-frequency hearing.

`${FIL%.*}.FFmpeg-Batch-Convert.mp4`        This sets the output container to .mp4.  To set it to a new container type, simply type the extension e.g. `.mkv`.  Note:  make sure the video/audio streams are compatible with the container.  See FFmpeg documentation.  Secondarily, this sets the output file name to the existing name appended by `FFmpeg-Batch-Convert` to make it easy to identify files that have been converted.

7.  Next, the script moves the files to the `CLEANUP` directory, named by default aptly `CLEANUP` and located one directory above the search directory.  If the `CLEANUP` directory doesn't exist, it's created.  It is important to ensure this directory is NOT within the path of the search since subsequent runs of the script convert those files again.  Note:  Ensure proper permissions are available to create the directory, when in doubt set it to the users home e.g. `~/CLEANUP` on Lines 715, 727, and 739.
8.  When the script has finished, it outputs a End of Script message.  This is useful when logging is enabled to tell if the script completed.

LOGGING:  adding a `tee` command to the script from the CLI or a cronjob is the easiest way to enable basic logging of terminal output (StdOut):

`FFmpeg-Batch-Convert.sh | tee -a ~/FFmpeg-Batch-Convert.log`

This will create a log file in the user's home directory, -a appends the file if it exists. To view this log use:

`cat ~/FFmpeg-Batch-Convert.log`

Avoid using nano or less commands to view the log file since the output will be messy due to the color coding commands.

As of right now, `-report` added to the FFMpeg string will produce a log file for each FFmpeg file conversion (rather messy).  Enhanced logging functionality is being worked on (Issue #3).
