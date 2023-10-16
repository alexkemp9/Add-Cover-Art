# Add-Cover-Art
A BASH Script to Add JPEG / WebP cover Art to a MP3 (music / podcast) file

![Steppes of Central Asia](Resources/folder.jpg)    
(above is the Cover Art used within the [MP3 file](Resources/AlexanderBorodin-Steppes-of-Central-Asia-Polovtsian-Dances-EvgenySvetlanov.mp3) within the [Resources directory](Resources)

The JPEG file above is what you see when the MP3 file within [Resources](Resources) is played. This cover-art was added using the [addCoverArt](addCoverArt) script file, and recovered today from the MP3 using a KID3 QML script-file:    

     kid3-cli -c "execute @qml /usr/share/kid3/qml/script/ExtractAlbumArt.qml" $PWD

## *Begin*
The following will assume that you have created a dir `~/.local/sbin` within which you store the bash-file; this is to set the script as executable for current user only:

```bash
$ chmod 0700 ~/.local/sbin/addCoverArt
$ la ~/.local/sbin/remove_ads
-rwx------ 1 user user 3205 Oct 15 17:42 /home/user/.local/sbin/addCoverArt
```
## *Help*
Attempting to run the bare script with zero parameters shows a brief Help message:

```bash
$ ~/.local/sbin/addCoverArt
Usage: addCoverArt MP3-file [JPG-file]
[Add JPEG cover art to an MP3 — music/podcast — file (1 or 2 parameters; this dir only)]
[WebP files are auto-converted to JPG; MP3 will retain same timestamp]
```
## *Usage*
You need both music/podcast + cover-art files within the same directory. To make life super-simple for yourself, name both files the same (except for the “.mp3”, “.jpg” : the TLS (3-letter suffix) at the end of each file). Then, with your command-prompt at the same dir that contains the files, run the script as follows:

```bash
$ chmod 0700 ~/.local/sbin/addCoverArt my-music-file my-cover-art-file
```
You can actually just run *“addCoverArt my-music-file”* (no quotes) if:    
1. '~/.local/sbin/' is within *$PATH*
2. Both *“my-music-file”* & *“my-cover-art-file”* have the same prefix

## *Extra Info*
The script is fairly basic. Check that the following assignments within the script match the locations within your computer (it will throw an informational error if not):     
- FILE="/usr/bin/file"
- FFMPEG="/usr/bin/ffmpeg"
- MP4DIR="/home/user/Videos"     
- (the above assumes that your MP3 are extracted from MP4 videos, and will auto-attempt to extract the mp3 if missing)
- MV="/bin/mv"
- RM="/bin/rm"
- TOUCH="/usr/bin/touch"
- TMP="./.addCoverArt.txt"  # temp timestamp file
- TMP3="./.addCoverArt.mp3" # temp MP3 file

## *WebP files*
A lot of image-files on the web that have *“.jpg”* TLS are actually WebP-format files (the TLS originated in Microsoft MSDOS, and was continued into MS Windows). However, web-browsers ignore the TLS & *“sniff”* the file to discover what type of file & which format it is.

A WebP image file can NOT be used as cover-art for a MP3 file. To handle that, the script *“sniffs”* all supplied cover-art-files. If they turn out to be WebP-format, then it will change the TLS to ‘.webp’ from ‘.jpg’. It will then use *ffmpeg* to change the format from WebP to JPEG. You thus need to make sure that you do NOT have both WebP & JPEG files with the same prefix-name in the same directory as your music/podcast files.

## *CAUTION!*
It *is* possible to add more than one image cover-art to the same music/podcast file. The music players that I have used will not recognise the 2nd cover-art.
