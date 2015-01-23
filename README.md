# FFmpeg-Batch-Convert
An FFMpeg bash script to batch convert video and audio files.  

Quick Note:  I recently branched off a dev branch and started work on a new interactive batch script (`FFmpeg-cron-converter`), so the repo is a bit messy per instant, apologies.  However,  the original project, `FFmpeg-batch-converter` in the `MASTER` branch, is still 100% functional and works well for both cron jobs or one-off batch processing.  The readme file `README-FFmpeg-Batch-Convert.md` is well organized.

This project consists of two scripts: an interactive bash script for one-off batch processing `FFmpeg-Batch-Convert.sh` AND a cron job designed to silently mantain a media library according to schedule (e.g. nightly) `FFmpeg-Cron-Convert.sh`.

Info here about diff between batch and cron
