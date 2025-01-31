![](logo3_256x256.png "Matroska logo")

# Matroska Test Files - Wave 1

This suite of files was created to validate the various Matroska players, parsers to make sure users get a consistent experience when moving their files on various programs/hardware. Since Matroska has a lot of features, it is hard to tell which are essential, which are encouraged and which are deprecated. The files presented here represent the minimum support a player should have to fully qualify as a Matroska player.

## Codecs

Matroska can support any codec that is around. That doesn't mean softwares should support all of them. For various reasons softwares and hardwares can't always be upgraded to support all codecs around. But in the other hand there are a few safe codecs that are often found in Matroska and WebM that should be supported. These codec can be found in various resolutions and features so even with the right codec support, it is not guaranteed that an implementation may support all the possibilities of a codec (it is hardly ever the case). This document will not cover codec details. But here is a list of codecs that are commonly found in Matroska:

### Video codecs

-    H264/AVC/MPEG4 Part 10, usually up to 1080p
-    MPEG4 Part 2, usually up to 720p
-    VP8, usually up to 720p
-    Theora, usually up to 720p

### Audio codecs

-    MPEG Audio Layer 3 (MP3)
-    Vorbis
-    AAC, AAC+, eACC+
-    AC-3
-    DTS
-    FLAC

### Subtitles codecs

-    plain UTF-8 text
-    ASS/SSA text
-    VOBSUB (bitmaps from DVDs)

## Audio only files

It is important to note that audio can also be used in audio only files, usually with the .mka extension. Those files should be handled as well, as long as the codec is supported.

## Extra features

There are a number of features that are not essential to the playback experience but could really improve it, like support for tags, cover art, embedded fonts, segment linking. We won't blame you if you don't support these, but your users/customers will probably ask for it at some point. There is also 3D support that is meant to grow in the coming years. Matroska should be able to support all the formats, but given the subject is really new, it's not covered by this suite of files.

## Test Files

### 1. Basic file

This file is the absolute minimum a compliant player should be able to handle.

The sample comes from the [Big Buck Bunny](http://www.bigbuckbunny.org/index.php/download/) open project. It contains MPEG4.2 (DivX) video, (854x480) MP3 audio, uses only SimpleBlock (matroska DocType v2)

*   [test1.mkv](test_files/test1.mkv)
*   [test1.mkv tags](test_files/test1-tag.xml)

### 2. Non default timecodescale & aspect ratio

This file has different features that need to be looked at carefully. The main one is the global TimecodeScale in the SegmentInfo is set to 100,000 rather than the default 1,000,000. That value affects the values of the file Duration in the Segment and the Clusters Timecode. The aspect ratio has also been stretched artificially to represent a 2.35 movie (from the original 16:9 aspect ratio). This file also contains CRC-32 values in the EBML header, the MetaSeek, the Segment Info, the Tracks and the Tags and PrevSize/Position in the Clusters for better error recovery.

It contains H264 (1024x576 pixels), and stereo AAC. The source material is taken from the [Elephant Dreams](http://orange.blender.org/download) video project

*   [test2.mkv](test_files/test2.mkv)
*   [test2.mkv tags](test_files/test2-tag.xml)

### 3. Header stripping & standard block

This file is using BlockGroup+Block only for audio and video frames. It also removes 2 bytes off each video and audio frame since they are all equal. These 2 bytes have to be put back in the frame before decoding. his file also contains CRC-32 values in the EBML header, the MetaSeek, the Segment Info, the Tracks and the Tags and PrevSize/Position in the Clusters for better error recovery.

It contains H264 (1024x576 pixels), and stereo MP3. The source material is taken from the [Elephant Dreams](http://orange.blender.org/download) video project

*   [test3.mkv](test_files/test3.mkv)
*   [test3.mkv tags](test_files/test3-tag.xml)

### 4. Live stream recording

This file is using the EBML feature that allows Master elements to have no known size. It is used for live streams because they don't know ahead of time the size of the Segment (virtually infinite) and even sometimes the size of the Clusters (no caching on the server side). The first timecode of the file also doesn't start at 0 since it's supposed to be a capture from something continuous. The SegmentInfo also doesn't contain any Duration as it is not know.

The sample comes from the [Big Buck Bunny](http://www.bigbuckbunny.org/index.php/download/) open project. It contains Theora video (1280x720), Vorbis audio, uses only SimpleBlock (matroska DocType v2)

A similar file can be created with [mkclean](http://www.matroska.org/downloads/mkclean.html) using the "--live" option

*   [test4.mkv](test_files/test4.mkv)
*   [test4.mkv tags](test_files/test4-tag.xml)

### 5. Multiple audio/subtitles

This has a main audio track in english and a secondary audio track in english. It also has subtitles in English, French, German, Hungarian, Spanish, Italian and Japanese. The player should provide the possibility to switch between these streams.

The sample contains H264 (1024x576 pixels), and stereo AAC and commentary in AAC+ (using SBR). The source material is taken from the [Elephant Dreams](http://orange.blender.org/download) video project

*   [test5.mkv](test_files/test5.mkv)
*   [test5.mkv tags](test_files/test5-tag.xml)

### 6. Different EBML head sizes & cue-less seeking

This file is a test of the EBML parser of the player. The size of the Segment and Block/SimpleBlock is coded using 1 (or the minimum possible the size) and 8 bytes randomly. The file also have no Cues entry. So seeking should be disabled or look for Cluster boundaries in the stream (much slower than using Cues).

The sample comes from the [Big Buck Bunny](http://www.bigbuckbunny.org/index.php/download/) open project. It contains MPEG4.2 (DivX) video, (854x480) MP3 audio, uses only SimpleBlock (matroska DocType v2)

*   [test6.mkv](test_files/test6.mkv)
*   [test6.mkv tags](test_files/test6-tag.xml)

### 7. Extra unknown/junk elements & damaged

This file contains junk elements (elements not defined in the specs) either at the beginning or the end of Clusters. These elements should be skipped. There is also an invalid element at 451417 that should be skipped until the next valid Cluster is found.

The sample contains H264 (1024x576 pixels), and stereo AAC. The source material is taken from the [Elephant Dreams](http://orange.blender.org/download) video project

*   [test7.mkv](test_files/test7.mkv)
*   [test7.mkv tags](test_files/test7-tag.xml)

### 8. Audio gap

This file has a few audio frames missing between timecodes 6.019s and 6.360s. The playback should not stop, and if possible the video should not be skipped where the audio is missing

The sample contains H264 (1024x576 pixels), and stereo AAC. The source material is taken from the [Elephant Dreams](http://orange.blender.org/download) video project

*   [test8.mkv](test_files/test8.mkv)
*   [test8.mkv tags](test_files/test8-tag.xml)

## Tools

All these files were created with [mkvmerge](http://www.bunkus.org/videotools/mkvtoolnix/) and [mkclean](http://www.matroska.org/downloads/mkclean.html). They also pass the [mkvalidator](http://www.matroska.org/downloads/mkvalidator.html) test tool (the test file 4 needs the --live option to correctly validate the file), except for the damaged file, as it is damaged.

## License

Both [Big Buck Bunny](http://www.bigbuckbunny.org/index.php/download/) and [Elephant Dreams](http://orange.blender.org/download) and licensed under the Creative Common License Attribution license, also known as CC-BY.

The recommended license text for Big Buck Bunny is `(c) copyright 2008, Blender Foundation / www.bigbuckbunny.org`.

The recommended license text for Elephant Dreams is `(c) copyright 2006, Blender Foundation / Netherlands Media Art Institute / www.elephantsdream.org`.

## Contact

If you have any question about these files please contact us at contact@matroska.org

## Changelog

-    2010-08-21: initial version
-    2016-06-03: moved to GitHub
-    2021-10-26: moved to IETF CELLAR working group
