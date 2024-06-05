# Matryoshka doll:-<br>
## [Link to question](https://play.picoctf.org/practice/challenge/129?category=4&page=1)
<br><br><br>
Description:- Matryoshka dolls are a set of wooden dolls of decreasing size placed one inside another. What's the final one? <br> Image: [dolls.jpg](https://mercury.picoctf.net/static/5ef2e9103d55972d975437f68175b9ab/dolls.jpg)<br>
1. Downloading the Image, it is a simple photo of a doll, nothing visibly notable.<br>
2. Looking at the exif data of the image using:<br>
<pre>
exiftool doll.jpg
</pre>
we get no notable information from the metadata of the image.<br>
3. Looking back at the question, it seems they want us to look for hidden files inside the image.<br>
4. Using binwalk to look at the information of the image:
<pre>
binwalk doll.jpg
</pre>
This gives us:
<pre>
binwalk dolls.jpg

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             PNG image, 594 x 1104, 8-bit/color RGBA, non-interlaced
3226          0xC9A           TIFF image data, big-endian, offset of first image directory: 8
272492        0x4286C         Zip archive data, at least v2.0 to extract, compressed size: 378954, uncompressed size: 383940, name: base_images/2_c.jpg
651612        0x9F15C         End of Zip archive, footer length: 22

</pre>
5. Looking at the third entry, we can see a zip file.
6. Using:
<pre>
binwalk -e dolls.jpg
</pre>
to extrat the archived data. This should create a file titled '_dolls.jpg.extracted' in the same directory.
7. To confirm, we can use ls command, getting :
<pre>
ls
_dolls.jpg.extracted  dolls.jpg 
</pre>


