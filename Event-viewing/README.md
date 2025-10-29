# Event-viewing:
Event-Viewing
Author: Venax

Description
One of the employees at your company has their computer infected by malware! Turns out every time they try to switch on the computer, it shuts down right after they log in. The story given by the employee is as follows:
They installed software using an installer they downloaded online
They ran the installed software but it seemed to do nothing
Now every time they bootup and login to their computer, a black command prompt screen quickly opens and closes and their computer shuts down instantly.
See if you can find evidence for the each of these events and retrieve the flag (split into 3 pieces) from the correct logs!
Download the Windows Log file here

Hints 
Try to filter the logs with the right event ID
What could the software have done when it was ran that causes the shutdowns every time the system starts up?

First, i check type file, after i used command to come enviroment of evtx-env to use command evtx_dump and i used command:
```
evtx_dump Windows_Logs.evtx > log.xml
```
And i open file log.xml by command:
```
code log.xml
```
After that i read through and see has an unusual passage:
```
&lt;string&gt;cGljb0NURntFdjNudF92aTN3djNyXw==&lt;/string&gt;
```
I try decode it and received one path of flag:
```
picoCTF{Ev3nt_vi3wv3r_
```
After that i filter with character "==" and i found the remaining two flags:
```
<Data Name="ObjectValueName">Immediate Shutdown (MXNfYV9wcjN0dHlfdXMzZnVsXw==)</Data>
<Data Name="param6">dDAwbF84MWJhM2ZlOX0=</Data>
```
decode it and tạe the flag
picoCTF{...}
