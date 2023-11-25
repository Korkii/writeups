We get this image.

![hideme_1](https://github.com/Korkii/writeups/assets/44523624/3dd821bf-24b1-43fe-b67d-46d1023207a8)
105657.png]]

We check using exiftool, 
![[Pasted image 20231112105710.png]]

There seems to be nothing here, maybe it's extension is not correct? 

![[Pasted image 20231112105740.png]]

Seems correct, lets try strings.
Yep! Look what we get: 

![[Pasted image 20231112105807.png]]

Lets use binwalk to extract it.

![[Pasted image 20231112105923.png]]

We open the flag image and we get this!
![[Pasted image 20231112105908.png]]

flag: picoCTF{Hiddinng_An_imag3_within_@n_ima9e_dc2ab58f}
