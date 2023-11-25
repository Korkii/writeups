We get this image.

![hideme_1](https://github.com/Korkii/writeups/assets/44523624/3dd821bf-24b1-43fe-b67d-46d1023207a8)


We check using exiftool, 
![[Pasted image 202![hideme_2](https://github.com/Korkii/writeups/assets/44523624/379e3127-0450-4dfb-9da6-58bdefe7d598)


There seems to be nothing here, maybe it's extension is not correct? 

![hideme_3](https://github.com/Korkii/writeups/assets/44523624/7f1e81b7-5766-47b5-9c7a-52ceed7a4514)



Seems correct, lets try strings.
Yep! Look what we get: 

![hideme_4](https://github.com/Korkii/writeups/assets/44523624/db73c3b7-1fff-43a6-8116-fdc2aed34970)


Lets use binwalk to extract it.

![hideme_5](https://github.com/Korkii/writeups/assets/44523624/1a95f181-a869-4223-bfde-0536ecbdde28)


We open the flag image and we get this!

![hideme_6](https://github.com/Korkii/writeups/assets/44523624/18edfc50-3f34-4892-9ff5-1648449ee8a1)


flag: picoCTF{Hiddinng_An_imag3_within_@n_ima9e_dc2ab58f}
