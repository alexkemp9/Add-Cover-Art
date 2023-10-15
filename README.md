# Add-Cover-Art
A BASH Script to Add JPEG / WebP cover Art to a MP3 (music / podcast) file

![Steppes of Central Asia](Resources/folder.jpg)    
(above is the Cover Art used within the MP3 file within the [Resources](Resources directory)

The JPEG file above is what you see when the MP3 file within Resources is played. This cover-art was added using the [addCoverArt](addCoverArt) script file, and recovered today from the MP3 using a KID3 inbuilt QEML script-file:
     kid3-cli -c " execute @qml /usr/share/kid3/qml/script/ExtractAlbumArt.qml " $PWD
