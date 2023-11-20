# *Scapy » ARP Storm
Category: Network Security
Level: easy
Points: 50

## Description

An attacker in the network is trying to poison the arp table of 11.0.0.100, the admin captured this PCAP.

 Link:https://hubchallenges.s3-eu-west-1.amazonaws.com/Forensics/ARP+Storm.pcap

install scapy
 ```fish
pip install scapy pyx --break-system-packages
 ```

 Add scapy directory to PATH. Add this to ```~/.config/fish/config.fish```
 ```
fish_add_path -g /home/shawal/.local/bin
 ```
Get the file
```
wget https://hubchallenges.s3-eu-west-1.amazonaws.com/Forensics/ARP+Storm.pcap
```
Now to analyse ARP+Storm.pcap

``` python 
scapy

>>> pkts = rdpcap('ARP+Storm.pcap')
>>> for pkt in pkts:
...:     print(pkt[ARP])

# we have arp code ipsource > ipdestination
# since code isn't default arp protocol(0 or 1)
# we explore the codes
>>> for pkt in pkts:
...:     print(list(str(pkt[ARP]).split(' '))[1])

# lets convert to ascii and eliminate newline end line character
>>> for pkt in pkts:
...:     print(chr(int(list(str(pkt[ARP]).split(' '))[1])),end='')
...: 
ZmxhZ3tnckB0dWl0MHVzXzBwY09kZV8xc19BbHdAeXNfQTZ1U2VkX3QwX3AwMXMwbn0=
# we get what looks like base 64 encoded value which we can decode

```
now to create a python script to return the encoded string which we can decode.

we open a file using 

```vim arp.py```

and paste the following code
```python
#!/usr/bin/python
from scapy.all import *
pkts = rdpcap('ARP+Storm.pcap')
for pkt in pkts:
     print(chr(int(list(str(pkt[ARP]).split(' '))[1])),end='')
```

now we make our script executable

``` 
chmod +x arp.py
```
now we can run and decode our script by 

```bash
./arp.py | base64 -d
```

we get 
```
flag{gr@tuit0us_0pcOde_1s_Alw@ys_A6uSed_t0_p01s0n}
```