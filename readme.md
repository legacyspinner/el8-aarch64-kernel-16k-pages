Wow , I just love to fix stuff that is not broken and to break stuff that is fixed!  :) As told by: My old boss.
<hr>

# DEVEL ONLY :
THIS IS NOT A STABLE VERSION, try the 4k version.
Unusual looping in some tests, maybe be video only not sure yet.

<hr>
<hr>
<hr>
<hr>
<hr>
<hr>
<hr>








For example, if you have
a el8-aarch64 installed already in UTM on a Apple M1 but its running in software mode.
That was the only way you could normally install 7/8 in UTM.
Now, you can install a new kernel or upgrade the old one and test with 16K pages.

It seems really fast to me as the 4K version does, now with 'Use Hypervisor' ticked.
*I assume this is the mac equivalent of KVM, but I could be wrong.


For configuration comparision:
In UTM I have 8 cores enabled with 8G memory.

This is the 16K pages version made specifically to match the apple m1 Native HW.
Kernel pagesize is also referred to by developers as granular translation table options or similar.

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
dnf install kernel
</code>

Reboot and check, if all went well:

If so you should see the following or similar.
Don't try the new kernel yet, until you check that "Use Hypervisor" box in UTM.
![8.8-on-Apple-Mac-M1-using-UTM](/assets/images/88-64k-utm-boot.png?raw=true)

Go ahead and shut down and enable better/faster/stronger Virtualization on your Mac M1 now :)
This is what you came for right? Then tick that little box that reads:
<code>
"Use Hypervisor"
</code>
*Ofc, we always wanted to 'use Hypervisor' on our aarch64/arm64 machines, now we can with all the el's  *7/8/9 :)
*7 yet to be rebuilt, but it will be.
**Updated: I've also starting checking 'Balloon Device' & 'use local time for base clock'

  ![8.8-on-Apple-Mac-M1-using-UTM](/assets/images/8.8UTM-VIRT-TICK.png?raw=true)

Then start up the machine again and you can check a couple things:
![8.8-on-Apple-Mac-M1-using-UTM](/assets/images/88-64k-utm-checks.png?raw=true)

Dmesg output:

![8.8-on-Apple-Mac-M1-using-UTM](/assets/images/88-64k-utm-dmesg1.png?raw=true)

![8.8-on-Apple-Mac-M1-using-UTM](/assets/images/88-64k-utm-dmesg2.png?raw=true)



Enjoy!

