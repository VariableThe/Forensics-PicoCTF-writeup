# This Document contains my solution and thought process for the information- forensic ctf.
<br>
The question can be found here (https://play.picoctf.org/practice/challenge/186?category=4&page=1)<br><br><br>
We start off by downloading cat.jpg.<br>
The description states *Files can always be changed in a secret way. Can you find the flag?*<br>
To get more information out of the image, I look into it's meta data<br>
There's nothing too out of the ordinanry until you look at the image resolution<br>
2560 x 1598<br>
2560x1598 is not a standard resolution. 2560 is usually paired with 1440<br>
Looking at the hint 2, we can see that the flag is 5 characters long<br>
Therefore it's not 1598<br>
Going back to look at metadata<br>
Analyzing the raw header gives no such lead <br>
Using base 64 decoding on the lisence field gives 'picoCTF{the_m3tadata_1s_modified}'<br>
Meaning we are searching the correct place.<br>
There's not really any other 5 digit number in the metadata.<br>
But the Information might be encoded in the raw header or the current_iptc_digest<br>
Both the raw header and the current_iptc_digest, decode to nonsense, when done so using base64<br>


