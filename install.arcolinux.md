




--
## create your own github version of ALIS
create desktop folder named AA; cd to this folder then
git clone the picoalis github url in this folder
rename it to the official name official-alis (for some comparison in the future)
you dont change anything in this folder
create a repo in github named mygh-alis (or equal)
git clone this inside the AA folder
copy the whole content of the folder alis to the 

NOTE: error cloning my created repo in local box as per below:
Cloning into 'myGH-alis'...
Username for 'https://github.com': eribertto
Password for 'https://eribertto@github.com': 
remote: Support for password authentication was removed on August 13, 2021. Please use a personal access token instead.
remote: Please see https://github.blog/2020-12-15-token-authentication-requirements-for-git-operations/ for more information.
fatal: Authentication failed for 'https://github.com/eribertto/myGH-alis.git/'

workaround:
followed this link https://stackoverflow.com/questions/68775869/support-for-password-authentication-was-removed-please-use-a-personal-access-to

success cloning with the CLI? yes # provide username, for password use the token below

token for 60 days expiration:
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





--
March 20, 2022
Install arcolinux arcolinuxl-v22.03.08-x86_64.iso in Thinkpad E590
This will overwrite the OS Manjaro Linux in partition 
/dev/nvme0n1 size 238.17 GB
Create swap (no hibernate) 8.80 GB
login name eribertto
passwd MKO00987ytr
use same password for the admin account


Note: Manjaro hanged while checking the partition details! Had to do a hard reboot to get it up again

Begin time: 1950
End time: 1958

Success installing the archlinux XFCE and do some tweakings. Also success building carli iso from eriks YT tutorial and booting to the build live usb. Note however that no network manager in the applet nor no gui web browser.

below is the reply of Erik arcolinux dev:
	Erik Dubois
	add any package from the Arch Linux repos to the list packages.x86_64
	neofetch is explained - carli project



After testing out the live iso i can reboot just fine to the 2 OS mxlinux and arcolinux XFCE.