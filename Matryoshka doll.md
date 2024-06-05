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
5. Looking at the third entry, we can see a zip file.<br>
6. Using:
<pre>
binwalk -e dolls.jpg
</pre>
to extrat the archived data. This should create a file titled '_dolls.jpg.extracted' in the same directory.<br>
7. To confirm, we can use ls command, getting :
<pre>
ls
_dolls.jpg.extracted  dolls.jpg 
</pre>
8. using cd to navigate into '_dolls.jpg.extracted':
<pre>
cd _dolls.jpg.extracted/
</pre>
9. using ls to look inside the file
<pre>
ls
4286C.zip  base_images
</pre>
10. We can see the file type using the file command:
<pre>
file base_images
base_images: directory
</pre>
<pre>
file 4286C.zip
4286C.zip: Zip archive data, at least v2.0 to extract, compression method=deflate
</pre>
11. We can see that '4286C.zip' is a zip archive data file and 'base images' is a directory, <br>according to the question- the flag should be in the next layer-, i.e. here the base images directory.<br>
12. using ls to look into the file gives us:
<pre>
ls base_images/
2_c.jpg
</pre>
13. There is only one image, it is the same image as the original one.<br>
14. Using binwalk on '2_c.jpg' gives:
<pre>
binwalk 2_c.jpg

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             PNG image, 526 x 1106, 8-bit/color RGBA, non-interlaced
3226          0xC9A           TIFF image data, big-endian, offset of first image directory: 8
187707        0x2DD3B         Zip archive data, at least v2.0 to extract, compressed size: 196045, uncompressed size: 201447, name: base_images/3_c.jpg
383807        0x5DB3F         End of Zip archive, footer length: 22
383918        0x5DBAE         End of Zip archive, footer length: 22

</pre>
15. Extracting the files:
<pre>
binwalk -e 2_c.jpg

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             PNG image, 526 x 1106, 8-bit/color RGBA, non-interlaced
3226          0xC9A           TIFF image data, big-endian, offset of first image directory: 8
187707        0x2DD3B         Zip archive data, at least v2.0 to extract, compressed size: 196045, uncompressed size: 201447, name: base_images/3_c.jpg
383807        0x5DB3F         End of Zip archive, footer length: 22
383918        0x5DBAE         End of Zip archive, footer length: 22

</pre>
16. Using ls to check directory:
<pre>
ls
2_c.jpg  _2_c.jpg.extracted
</pre>
17. repeating steps 11 to 13, we get the same image again inside the zip file:
<pre>
cd _2_c.jpg.extracted/
</pre>
<pre>
ls
2DD3B.zip  base_images
</pre>
<pre>
cd base_images/
</pre>
<pre>
ls
3_c.jpg
</pre>
18. We have now reached the third photo.<br>
19. repeating steps 14 through 16 again:<br>
20. We get '4_c.jpg'<br>
21. using binwalk on this gives:
<pre>
binwalk 4_c.jpg

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             PNG image, 320 x 768, 8-bit/color RGBA, non-interlaced
3226          0xC9A           TIFF image data, big-endian, offset of first image directory: 8
79578         0x136DA         Zip archive data, at least v2.0 to extract, compressed size: 64, uncompressed size: 81, name: flag.txt
79786         0x137AA         End of Zip archive, footer length: 22

</pre>
22. As it is visible, the zip file contains flag.txt.<br>
23. Extracting the zip file, navigating into it and reading flag.txt gives us:
<pre>
cat flag.txt
picoCTF{e3f378fe6c1ea7f6bc5ac2c3d6801c1f}
</pre>
24. Here the flag is 'picoCTF{e3f378fe6c1ea7f6bc5ac2c3d6801c1f}'
25. Submitting the flag completes the question.






