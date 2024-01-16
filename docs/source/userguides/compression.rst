==========================
Compression Overview
==========================

Compressing data is basically a required action nowadays. Keeping your dataset around in its raw state would be nigh impossible for most data storage capabilities. 
So we compress data, for the sake of any SAN administrators and Sys-Admins fighting to keep their storage space from collapsing under their 
collective weight of research datasets. 

Broadly speaking, you get have two main types of things we want to compress in some way: 

#. Text 
#. Video

Lets not get into Images/TIFFs, as i've never had good results with attempting to compress multi-layer Geo-Tiff's. Just treat images as a 'Text' file, but expect
the compression ratio to be somewhere between 'meh' and 'abysmal'. 

Also, yes I *know* the correct term for *video compression* is *re-encoding*, but lets not argue semantics. 


Compression Trade-Offs 101
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
If you are compressing something, then something has to give. It usually boils down to a few points that you get to slide between. 

#. Computation Time 
#. Size of Output / Amount of Reduction 
#. Quality of Output 

Its (almost) the old adage of 'Quick, Fast, Cheap', pick one - the only change is usually, you can pick two *especially for video*. So it plays out, **in very general terms**, somewhat like so: 

#. No Computation time, keep the quality? You get a massive file size
#. Lots of Computation time, keep the quality? You get small file size
#. Lots of Computation time, drop some quality? teeny tiny file size 

So you get the idea - spend more time to do a thing, and it will, on average, be smaller at the end of it. 


=========================
Video Compression 
=========================
Starting with video, as video is *complicated*. This guide is very much **not** a guide on filters, codec differences, hardware vs. software encoding, HDR, CMYK, 4:4:2 vs 4:4:4 chroma or anything of that. So, to be very clear, 
this will *not be covering*: 

#. Chroma Encoding / Gamut / Colour spaces / etc. 
#. VBR vs CBR 
#. Filters of *any sort* 
#. Debate about FOSS/Open vs. Closed vs. Semi-Closed Codec 
#. Upscaling / Super-Resolution Style Enhancements 
#. X-Special-Presets for Y-Tooling 
#. Matroska vs. Mpeg vs. WebM vs. Whatever-Container-You-Champion

What we will cover is going to meet the following criteria: 

#. Simple, User Friendly, Cross-Platform and preferably with a GUI
#. A quick list of Key-Terms, 
#. A very rough idea of how to get 'Acceptable' results 

Before we dive too deep. Video encoding will generally take a *very, very long time*. So best you have access to a nvidia GPU of some description, or have a decent workstation that you can throw this at a queue of jobs
and just leave it alone for as long as it takes to crunch. You'll also need disk space a plenty - SSD's will make sure you don't get held of by spinning rust. 

The NVidia hardware encoder is widely supported, and called NVENC. Funnily enough, the decoder is NVDEC.  


Tooling Choice 
^^^^^^^^^^^^^^^^^^^^^^^^

.. _Handbrake: https://handbrake.fr/

Handbrake_ wins hands down for tooling. Its cross platform, supports GPU Acceleration, and can just about convert anything to anything for video. So grab it via your preferred installation method. Its been around 
for almost as long as the dinosaurs, and does support all the fancy features, like HDR. Which we don't actually care about at this stage, but now you know the tooling has the chops for production level things. 

Its also loaded with a bunch of presets that make your life *much* easier, as they have already done all the hard work around dialling in the settings and tweaking the million dials for you. 


Video Compressions: The Moving Parts
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Video compression is mainly governed by the codec used. Codec is short-hand for enCOder-DECer: CO-DEC. So its made of both the encoder, to create the video file, and the decoder, to play it back. 
As with all things, there are proprietary and open codecs. Generally, the newer the better, but newer also usually means 'more compute time'.  Generally, the best-to-worst is as follows for file-size: 

#. AV1 
#. VP9
#. H265 (HEVC)
#. H264 (AVC)

Then we have a container of some description. The container is just 'how do we hold and describe the video, audio and subtitle channel' type thing. You put a video stream, some audio streams, and maybe subtitles into a container. That is it, job done. 

So, to summarise, you have control over: 

#. The Codec
#. The Container 


Resolutions and You
^^^^^^^^^^^^^^^^^^^^^^
While usually, video will list both the pixel resolution and the short-hand friendly name, but not always. Here is a list for you, in the format of <Short Name, Length x Width in Pixels, Acronym>

#. 1080P, 1920x1080, Full-HD / HD 
#. 2160P, 2560x1440, QWHD 
#. 3160P, 3840x2160, UHD 


Compressing Video: The Quick Guide
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Handbrake is very easy to use. You can point it at a folder to convert *everything* in that folder, or a single file at a time. The steps are the same, so we will work with a single file for now. And use a preset, to make life
easier all around. 

1. Open Handbrake
2. Click 'Open Source', then select the Video File you want to compress.
3. Wait for Handbrake to open and parse the file 
4. At the top the screen, there is a "Preset" Drop-Down list. 
5. Select the preset you would like. 
6. In the 'Format' Drop-Down, change the container if you like. MKV is generally a little more forgiving for playback than mp4, anecdotally. 
7. Hit 'Start' Encode 
8. Wait

That's it. The longer video encoding version will be written if and when I get enough interest in pick-everything-manually-process.

Now, onwards! Text compression is must less complicated for the quick version. 


========================
Text Compression
========================
Text (or just general files) is usually simpler than video compression. Again, its governed by the algorithm used, and the universal trade-off - but this time, 
its just the two dimensions of file size and computation time. So, we will start with the algorithms, them move on to tooling. 


File Compression Algorithms 101
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Generally, the newer algorithms have better compression. However, the highest-is-not-always-the-absolute-best, although we are talking low single-digit percentage difference in final file-size. 
The usual difference is the exponential difference in computation time. So in VERY rough best-to-worst-on-vague-average, we can talk about the following algorithms. For all that is good, 
this is just a **rough** estimate. I did say it (file compression) was simpler than video, but compression is still complicated - so this list *is not always truth*. Do not treat it as such!

#. LZMA2 and LZMA (V2 is better at multi-threaded compression)
#. BZIP 
#. ZSTD 
#. GZIP/ZIP 

File Compression Tooling: GUI
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Compression tools with a GUI has multiple options, but this guide assumes 7zip.  It's got support for most of the algorithms listed above, is cross-platform and has a nice user interface. 
Using 7zip is the same as any other compression program - add files to your archive as you want. For best results, you want to avoid .zip , the compression ration is usually hot garbage 
compared to newer algorithms - only use .zip if you must have an absolutely *ancient* system decompress the file - this includes GNU zip/.gzip/.gz files. 

#. AVOID using .zip or .gzip
#. Use the .7z, .xz or .bzip2 archive types - they will use a decent compression algorithm by default
#. Ramp up the 'Compression Level' to your wanted level of time-to-compress vs. file-size
#. Hit OK, and wait for you shiny new archive 

As a rough 'real-world' example, a 1.2GB of python, bash and CSV data-files was compressed, using 7zip, with compression level 'Ultra' to about 45MB. Yes, that's 1200MB down to 45MB. Text 
will compress down to almost nothing. Only took a few minutes to compress on a decently powerful desktop. 


File Compression Tooling: Somewhat-Modern CLI 
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
For any unix-like system, you will almost certainly have access to the program ``tar``. There are multiple versions and flavours of this program with slightly different options. For best usage
I strongly suggest the RTFM (read the *friendly* manual) approach available via ``man tar``. This guide assumes GNU Tar. When using ``tar``, older version do not support the direct creation of archives, 
so the command is slightly different. And, there are two ways of giving it options to control what ``tar`` does. You have ``tar -optionslist`` and ``tar optionlist``. 
I.e., with and without the ``-`` character. *There is a difference**. If in doubt, RTFM. 

When using the ``-`` the ``f`` for 'Filename' **must come last**. The below commands assume that you can use a somewhat recent vertsion of ``tar`` that supported 
direct archive creation. 

#. ``tar -cJf archivename.xz /path/to/thing/to/compress/`` 

When not using the ``-``, the it doesn't matter the order. 

#. ``tar fcJ archivename.xz /path/to/compress/``


Now, onwards, to a quick list of options. If its a single letter, you can use it with or with the `-`. If it has ``--option``, you need the `--`.
**Case. Is. IMPORTANT**. Let that be your first and only reminder/warning. 


GNU Tar: Quick CLI Options List 
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
A quick list of CLI options. Again, RTFM via ``man tar`` if want to fine-tune it. 

+---------------+--------------------------------------------------------------------------------------------------------------+
| Option Letter |  What it does                                                                                                |
+===============+==============================================================================================================+
|      J        | Create a XZ Archive                                                                                          |
+---------------+--------------------------------------------------------------------------------------------------------------+
|      j        | Create a BZIP2 Archive                                                                                       |   
+---------------+--------------------------------------------------------------------------------------------------------------+
|      a        | Guess the arhive program to use, by looking at the file suffix, eg ``archive.xz`` is the same as using ``J``.|
+---------------+--------------------------------------------------------------------------------------------------------------+
|     --lzma    |  Create a lzma Archive                                                                                       |
+---------------+--------------------------------------------------------------------------------------------------------------+


As a rough real-world example for you: Using XZ, with level 9e, and 12 threads, it took about a day to compress 1.2TB of assorted Geo-Tiff and CSV data file down to about 700MB.