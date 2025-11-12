# Torrent Analyze
Torrent Analyze
Author: Mubarak Mikail

Description
SOS, someone is torrenting on our network.
One of your colleagues has been using torrent to download some files on the company’s network. Can you identify the file(s) that were downloaded? The file name will be the flag, like picoCTF{filename}. Captured traffic.
Hints 
Download and open the file with a packet analyzer like Wireshark.
You may want to enable BitTorrent protocol (BT-DHT, etc.) on Wireshark. Analyze -> Enabled Protocols
Try to understand peers, leechers and seeds. Article
The file name ends with .iso

First we wget challenge and open it by wireshark, because challenge suggest is protocol BT-DHT so we just focus it, and if wireshark of you don't see it, please click Analyze -> Enabled Protocols
. And we have to remember this, we are looking for file name, not file content, that has been downloaded, not share by someone in our network. So we just focus info hash of packets, we are easy to 
relize info_hash appear many times, after we need copy hash and search it in google and we will see file name. 
<img width="804" height="177" alt="image" src="https://github.com/user-attachments/assets/fc461cf0-2668-45c2-827a-3bf7affaa703" />
