Current Graphics Card: AMD Radeon (Using AMDGPU not AMDGPU PRO)

## Adding a few kernel parameters
edit the `/etc/default/grub` \
and navigate to the line having `GRUB_CMDLINE_LINUX_DEFAULT=""` and then add the following after anything already present there  

to get dynamic power management(DPM)
~~~
amdgpu.dpm=1
~~~

tweaking performance by enabling Display Cores
~~~
amdgpu.dc=1
~~~

then update the grub configuration
~~~
sudo grub-mkconfig -o /boot/grub/grub.cfg
~~~

then reboot
~~~
sudo reboot
~~~

then verify if the kernel parameters were applied
~~~
cat /proc/cmdline
~~~
the added parameters should be listed among boot parameters

## Making a Xorg Configuration file
will be located at `/etc/X11/xorg.conf.d/20-amdgpu.conf` \
add this to the file
~~~
Section "OutputClass"
     Identifier "AMD"
     MatchDriver "amdgpu"
     Driver "amdgpu"
     Option "EnablePageFlip" "off"
     Option "TearFree" "false"
EndSection
~~~

this enable Tear-Free video playback for minimizing screen tearing \
and also disables page flipping to minimize output latency 

