# Find And Open
FindAndOpen
Author: Mubarak Mikail

Description
Someone might have hidden the password in the trace file.
Find the key to unlock this file. This tracefile might be good to analyze.
debug info: [u:723551 e: p: c:348 i:294953]

Hints 
Download the pcap and look for the password or flag.
Don't try to use a password cracking tool, there are easier ways here.

First i read file pcap and i realize there was sth difference, i copy it and decode and received string: This is the secret: picoCTF{R34DING_LOKd_
, and i try take it to unzip file flag and i received complete flag:
picoCTF{R34DING_LOKd_fil56_succ3ss_cbf2ebf6}
