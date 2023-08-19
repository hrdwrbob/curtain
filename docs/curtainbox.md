
Dedicated linux machine for audio routing, configured and managed via web interface, but with support for displays and and interface devices etc etc
Can be run on existing linux machines, but ideally on dedicated HW so you get low latency etc.
backend for all audio is pipewire.
... actually you could purely use it as a network audio router.
Distribution: docker container, bare metal installation (based on ???)

System intentions:

48k input
96k internal
96/48k output.
96k allows you to cache more frames for processing with less impact on overall latency, to allow more advanced filtering and reduce aliasing. It is not required for 


General Hardware:
x86 linux
USB audio.
Firewire optional for interfaces/mixer.
HDMI Audio output.
Could be run on pi, but you won't be able to use many filters etc due to limited CPU.


My Hardware:
system (12V out to projectmix)
Source Display
ProjectMix I/O (out to zone 2 reciever, in from mic. in from other systems in stereo)
HDMI out to receiver