# Informantion:-
## [question link](https://play.picoctf.org/practice/challenge/186?category=4&page=1)
<br>
**Description:-** Files can always be changed in a secret way. Can you find the flag? <br>
Image: [cat.jpg](https://mercury.picoctf.net/static/b4d62f6e431dc8e563309ea8c33a06b3/cat.jpg) <br>
1. Downloading the image we see the photo of a cat.<br>
2. looking at the metadata of the file using exiftool:
<pre>
exiftool cat.jpg
ExifTool Version Number         : 12.76
File Name                       : cat.jpg
Directory                       : .
File Size                       : 878 kB
File Modification Date/Time     : 2024:06:05 22:51:11+05:30
File Access Date/Time           : 2024:06:05 22:51:19+05:30
File Inode Change Date/Time     : 2024:06:05 22:51:13+05:30
File Permissions                : -rw-r--r--
File Type                       : JPEG
File Type Extension             : jpg
MIME Type                       : image/jpeg
JFIF Version                    : 1.02
Resolution Unit                 : None
X Resolution                    : 1
Y Resolution                    : 1
Current IPTC Digest             : 7a78f3d9cfb1ce42ab5a3aa30573d617
Copyright Notice                : PicoCTF
Application Record Version      : 4
XMP Toolkit                     : Image::ExifTool 10.80
License                         : cGljb0NURnt0aGVfbTN0YWRhdGFfMXNfbW9kaWZpZWR9
Rights                          : PicoCTF
Image Width                     : 2560
Image Height                    : 1598
Encoding Process                : Baseline DCT, Huffman coding
Bits Per Sample                 : 8
Color Components                : 3
Y Cb Cr Sub Sampling            : YCbCr4:2:0 (2 2)
Image Size                      : 2560x1598
Megapixels                      : 4.1
</pre>
3. The license looks very suspicious and abnormal.<br>
4. Decoding the license using base64 decoding:
<pre>
echo cGljb0NURnt0aGVfbTN0YWRhdGFfMXNfbW9kaWZpZWR9 | base64 --decode
picoCTF{the_m3tadata_1s_modified}                                                                               
</pre>
5. 'picoCTF{the_m3tadata_1s_modified}' is the flag and submission is accepted

