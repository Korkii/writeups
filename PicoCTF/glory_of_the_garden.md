
After running exiftoool, we see that except for 1 link there's nothing here.

![](Pasted%20image%2020231112102254.png)

We check the link and it doesn't seem to be related to the image.

![](Pasted%20image%2020231112102419.png)

Maybe the file is not what it says it is? We check using file.

![](Pasted%20image%2020231112102505.png)

Nothing suprising, we move on to checking the strings of the image.

![](Pasted%20image%2020231112102533.png)

And right at the end, we got the flag! 

flag: `picoCTF{more_than_m33ts_the_3y33dd2eEF5}`