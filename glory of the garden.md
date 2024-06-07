# Glory of the garden:
## [question](https://play.picoctf.org/practice/challenge/44?category=4&page=1)
## [image](https://jupiter.challenges.picoctf.org/static/4153422e18d40363e7ffc7e15a108683/garden.jpg)

Description: This garden contains more than it seems.

Downloading the image, it is just a photo of a garden.
Using exiftool:

<pre>
exiftool garden.jpg
ExifTool Version Number         : 12.76
File Name                       : garden.jpg
Directory                       : .
File Size                       : 2.3 MB
File Modification Date/Time     : 2024:06:07 09:05:23+05:30
File Access Date/Time           : 2024:06:07 09:05:25+05:30
File Inode Change Date/Time     : 2024:06:07 09:05:23+05:30
File Permissions                : -rw-r--r--
File Type                       : JPEG
File Type Extension             : jpg
MIME Type                       : image/jpeg
JFIF Version                    : 1.01
Resolution Unit                 : inches
X Resolution                    : 72
Y Resolution                    : 72
Profile CMM Type                : Linotronic
Profile Version                 : 2.1.0
Profile Class                   : Display Device Profile
Color Space Data                : RGB
Profile Connection Space        : XYZ
Profile Date Time               : 1998:02:09 06:49:00
Profile File Signature          : acsp
Primary Platform                : Microsoft Corporation
CMM Flags                       : Not Embedded, Independent
Device Manufacturer             : Hewlett-Packard
Device Model                    : sRGB
Device Attributes               : Reflective, Glossy, Positive, Color
Rendering Intent                : Perceptual
Connection Space Illuminant     : 0.9642 1 0.82491
Profile Creator                 : Hewlett-Packard
Profile ID                      : 0
Profile Copyright               : Copyright (c) 1998 Hewlett-Packard Company
Profile Description             : sRGB IEC61966-2.1
Media White Point               : 0.95045 1 1.08905
Media Black Point               : 0 0 0
Red Matrix Column               : 0.43607 0.22249 0.01392
Green Matrix Column             : 0.38515 0.71687 0.09708
Blue Matrix Column              : 0.14307 0.06061 0.7141
Device Mfg Desc                 : IEC http://www.iec.ch
Device Model Desc               : IEC 61966-2.1 Default RGB colour space - sRGB
Viewing Cond Desc               : Reference Viewing Condition in IEC61966-2.1
Viewing Cond Illuminant         : 19.6445 20.3718 16.8089
Viewing Cond Surround           : 3.92889 4.07439 3.36179
Viewing Cond Illuminant Type    : D50
Luminance                       : 76.03647 80 87.12462
Measurement Observer            : CIE 1931
Measurement Backing             : 0 0 0
Measurement Geometry            : Unknown
Measurement Flare               : 0.999%
Measurement Illuminant          : D65
Technology                      : Cathode Ray Tube Display
Red Tone Reproduction Curve     : (Binary data 2060 bytes, use -b option to extract)
Green Tone Reproduction Curve   : (Binary data 2060 bytes, use -b option to extract)
Blue Tone Reproduction Curve    : (Binary data 2060 bytes, use -b option to extract)
Image Width                     : 2999
Image Height                    : 2249
Encoding Process                : Baseline DCT, Huffman coding
Bits Per Sample                 : 8
Color Components                : 3
Y Cb Cr Sub Sampling            : YCbCr4:2:0 (2 2)
Image Size                      : 2999x2249
Megapixels                      : 6.7
</pre>

No useful information or anything out of the ordinary.

Using binwalk to check for additional information:

<pre>
binwalk garden.jpg

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             JPEG image data, JFIF standard 1.01
382           0x17E           Copyright string: "Copyright (c) 1998 Hewlett-Packard Company"
</pre>

Looks normal, nothing out of the ordinary here as well.

Taking a look at the hint for the question it says: 'What is a hex editor?'<br>
Using hexdump (bad mistake, should have used hexdump -C instead)<br>
Gives an incredibly long output of gibberish.<br>
Using strings command and grep to find 'picoCTF' as the flag contains picoCTF:

<pre>
strings garden.jpg | grep 'picoCTF'
Here is a flag "picoCTF{more_than_m33ts_the_3y33dd2eEF5}"
</pre>

We get a hit and it returns the flag.
Submitting 'picoCTF{more_than_m33ts_the_3y33dd2eEF5}' works and is accepted.

**P.S. I had the opportunity to look at other writeups, until now I've only written about what has worked, but I will now also be including everything I try including the massive failures :)**
