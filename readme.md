# 16K pages, BUILDING NOW! DO NOT USE THIS YET.
# This was cloned from my 4K repo of same name, NOT DONE YET.
# *snagged a bug quick, I'll work this out soon.
# *I think it came from my UNCLEAN HOST Target I installed from that had too much muck in /boot and EFI
# *I'll remove this message if a clean host install works from the repo install.

<hr>
<hr>

Wow , I just love to fix stuff that is not broken and to break stuff that is fixed!  :) As told by: My old boss.
<hr>

# To test it in a virtual environment on a el8.x aarch64 install. 

For example, if you have
a el8-aarch64 installed already in UTM on a Apple M1 but its running in software mode.
That was the only way you could normally install 7/8 in UTM.

Now, you can install a new kernel or upgrade the old one and test with 16K pages.

It seems really fast to me, now with 'Use Hypervisor' ticked.

*I assume this is the mac equivalent of KVM, but I could be wrong, I'm sure I will be corrected if so!

I also have 8 cores enabled with 8G memory.

*Next up lets see how fast the M1 can go on UTM with el8, with native 16K pages, w00t!
I did this so I could build faster packages for the Rpi's, before It would take me over a day to compile
a kernel native on a RPi4, or a not very long with CROSS ofc, but I dont want to use cross. I wanted NATIVE
and now I have it! For testing only ofc, bugs included! Soon, I'll get back to my goal when I started this, 
which spawned from another project. Hopefully now I can make arm packages NATIVE and FAST. 


***UPDATE: Yes, my mac m1 with UTM running el8 on aarch64 is blazing fast now! I just rebuilt this projects
kernel in less than an hour! Host didnt crank on its fan very much, that I could hear :)

***2nd test run: btop shows the host Apple OS with m1 running 96% cpu at 70 deg c, with a loag avg right now of , 9.2 7.4, 6.18
So the hardware is being utilized very well. 


This is fast/per watt, really fast!

*I'm going to bump the spec and time it now!
Testing123:
<code>
time rpmbuild -ba --target=$(uname -m) kernel.spec --without debug --without debuginfo --without kabichk kernel.spec 2> build-err.log | tee build-out.log
</code>

Results:
Ok ~15min. Checking again to confirm.








See for yourself! Ready set go?
<hr>
<hr>
On your UTM installed el8, to test/install to new 16K pages kernel:


From your test install(not production box):

create the file for the repo @:
<code>
/etc/yum.repos.d/el8-aarch64-16k-pages.repo
</code>

with the contents:
<code>
[el8-aarch64-16k-pages]
name=el8-aarch64 w/16k CPU PAGES repo 
baseurl=https://sourceforge.net/projects/el8-aarch64-16k-pages-repo/files/dnf/8/
gpgcheck=0
enabled=1
</code>

Then run:
<code>
yum install kernel
</code>

Reboot and check, if all went well:


If so you should see the following or similar.
![8.8-on-Apple-Mac-M1-using-UTM](/assets/images/88-64k-utm-boot.png?raw=true)

Go ahead and shut down and enable better/faster/stronger Virtualization on your Mac M1 now :)
This is what you came for right? Then tick that little box that reads:
<code>
"Use Hypervisor"
</code>

*Ofc, we always wanted to 'use Hypervisor' on our aarch64/arm64 machines, now we can with all the el's  *7/8/9 :)
*7 yet to be rebuilt, but its easy peasy.

  ![8.8-on-Apple-Mac-M1-using-UTM](/assets/images/8.8UTM-VIRT-TICK.png?raw=true)

Then start up the machine again and you can check a couple things:
![8.8-on-Apple-Mac-M1-using-UTM](/assets/images/88-64k-utm-checks.png?raw=true)

Dmesg output:

![8.8-on-Apple-Mac-M1-using-UTM](/assets/images/88-64k-utm-dmesg1.png?raw=true)

![8.8-on-Apple-Mac-M1-using-UTM](/assets/images/88-64k-utm-dmesg2.png?raw=true)



Enjoy!

