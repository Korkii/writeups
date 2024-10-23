
## The Challenge

_Category_: Traffic Analysis
_Number of Points:_ 250
_Challenge Name:_ Unusual Exfiltration
_Challenge Description:_ `Network logs from a machine DEADFACE compromised are being analyzed. It seems something was exfiltrated to their proxy machine on the local network before being sent back to their C2 server. Can you help figure out what data was stolen?

![](Pasted%20image%2020241023074221.png)

## Solution

Another pcapng file challenge... huh.
Whenever I solve this ~~bad~~ great category, I always have a few stuff that I like to check.
- If the file is a pcapng file, it's able to have comments, so checking them might be useful in case they hid something in there
- The protocol hierarchy

After checking the first one, we check the protocol hierarchy :D
You can access it through `Statistics -> Protocol Hierarchy`

![](Pasted%20image%2020241023074922.png)

From this image we can understand we have a lot of data, so lets filter for it.

![](Pasted%20image%2020241023091721.png)

A quick note - _A stream refers to the flow of data back and forth over the course of a protocol conversation between two endpoints_.

Furthermore, if we follow one of the streams we will see that it sends a message containing the letters 'Q' and 'R', and the destinations responds with an `'ack'` signal, for approval.

![](Pasted%20image%2020241023075307.png)

So from here the solution is obvious right? Nope! For some random reason it took a few hours of watching Frieren for the lightbulb to light up in my brain. 
The letters 'Q' and 'R' refer to a QR code, however, when you print the data section of the packets you don't necessarily see that.

![](Pasted%20image%2020241023091753.png)

In order to print that, I wrote this little script:

```python
from scapy.all import rdpcap, IP


pcap_file = 'unusualexfil.pcapng'
output_file = 'enc.txt'
packets = rdpcap(pcap_file)

target_ip = '192.168.50.135'

with open(output_file, 'w') as f:
    for packet in packets:
        if IP in packet and packet[IP].src == target_ip:
            if packet.haslayer('Raw'):
                data = packet['Raw'].load
                f.write(data.decode('utf-8', errors='ignore'))
```

And after trying to read it like a binary ( that was before the lightbulb lit up ), I finally read it normally using this script: 

```python
from PIL import Image

with open('enc.txt', 'r') as file:
    input_data = file.readlines()

size = max(len(line.strip()) for line in input_data)

qr_image = Image.new('1', (size, size), 1)

pixels = qr_image.load()
for y, line in enumerate(input_data):
    for x, char in enumerate(line.strip()):
        if char == 'Q':
            pixels[x, y] = 0
        else:
            pixels[x, y] = 1

qr_image.save('qr_code.png')
```

And I received this image:

![](Pasted%20image%2020241023080225.png)

When putting it into a QR reader online, you receive the flag :)

![](Pasted%20image%2020241023080358.png)

Flag: `flag{QR-c0de-4-exfiltr@ation}`

![](white-dream-personal-use-only-regular-1.png)