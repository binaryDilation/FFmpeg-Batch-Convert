# FFmpeg-Batch-Convert
100% Working.  An FFMpeg bash script to batch convert video and audio files.  Interactive or Crontab.

This project consists of two scripts: an interactive bash script for one-off batch processing `FFmpeg-Batch-Convert.sh` AND a script optimizde for use as a cron job, `FFmpeg-Cron-Convert.sh`, designed to silently mantain a media library according to a crontab schedule (e.g. nightly).  The readme files for each script, `README-FFmpeg-Batch-Convert.md` and `README-FFmpeg-Cron-Convert.md`, are the next place to look for setup, usage, and functionality.

Quick Note:  I recently branched off a new dev branch and started work on morefeature-rich interactive batch script (`FFmpeg-Batch-Converter`), so the repo is a bit messy per instant, apologies.  However,  `FFmpeg-Cron-Converter` in the `MASTER` branch, is still 100% functional and works well for both cron jobs or one-off batch processing.  The readme file `README-FFmpeg-Cron-Convert.md` is well organized.  `FFmpeg-Batch-Converter`, the interactive script, is also 100% functional, but the readme hasn't been updated yet for the new changes.

Difference: The intractive script prompts the user for the location of the search directory, whether they desire a recursive search, etc., whereas the cron script stores that hardcoded into the script.  Both the batch and cron script at find at doing one-off batch processing, but some less-experienced users may prefer the interactive prompts vs. editing a shell script.
