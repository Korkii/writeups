This file is obviously a powerpoint presentation, so I look through strings in order to find hidden strings.

![](Pasted%20image%2020231112102933.png)

And there we go!
Now using binwalk we will extract the files.

![](Pasted%20image%2020231112104000.png)

And from there we can simply navigate to the requested folder and cat the hidden text.

![](Pasted%20image%2020231112104047.png)

It seems like an encypted message, lets remove the spaces. 

![](Pasted%20image%2020231112104410.png)

And it seems like a base64 string, lets decode it.

![](Pasted%20image%2020231112104706.png)

And we got our flag!

flag: `picoCTF{D1d_u_kn0w_ppts_r_z1p5}`