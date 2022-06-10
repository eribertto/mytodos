hi everyone i hope this video finds you
well
and today we are going to talk about
snapshots on endeavor os now enable os
released a new iso a few days ago and
i'm gonna do a separate video about that
but in this specific video i'm going to
show you how you can install time shift
on endeavor os using the battery fs file
system and basically taking snapshots
and snapshots during system updates so
without too much talking let's jump into
the video so this is a default installation of
endeavor os atlantis which just came out
a few days ago
and i will leave a link in the video
description below to the website of
never os where you can download the iso
now endeavor os has become very popular
as you probably already know it's an
arch based distribution and in this
video here i've installed a fresh copy
of endeavor os gnome which is installing
actually gnome 41.2
but what i'm going to show you in this
video it's going to work whether you're
choosing gnome or any other desktop
environment now the important thing here
is that when you install the endeavor os
you use the butterfest file system now
let me pull up the terminal here and let
me go full screen so that you can see
better so if i increase the font sizes
so let me type in lsblk
because i want to show you here the
layout of the disk now when i installed
here endeavor os i chose actually the
battery fs file system and a swap file
and you can see here by default these
are the sub volumes that were created
now we can list the sub volumes here if
we use the butterfest subwool list
command which i already run before here
so you can pause the video here if you
want to mark down this command here so
butter the face of all list and then the
slash is going to show you all the sub
volumes in the system so when i hit
enter here i need to authenticate
because i'm using sudo and as you can
see here we have several sub volumes so
we have the roots of volume home cache
log and the swap which is actually the
swap file
now if i want to see the fstop file here
i can use the cat command cat etsy slash
fstab
is going to show you the fstop file here
for the system let me make this a little
smaller
so that we can see the options here on
the right side of the display you can
see here we have the default options on
how endeavor os installs we have no a
time auto defrag and compression is that
std now there are some other options
which are not present here for example
space cache nevertheless it's really a
good set of options that we have here so
having the bada fast file system here
it's a very nice if you want to take
also snapshots now by default actually
endeavor os does not come installed with
timeshift
but you can installing using the ea
helper which is already pre-installed in
endeavor os so when you type in here yay
in the terminal it's going to check for
updates for the system and also for
packages on the aur right now there is
just one here we just came out probably
a few minutes ago because the install is
pretty fresh so i'm just going to
install it very quickly here
and so when you are up to date and you
run yay again you will see nothing
basically there is nothing to do
but time shift is available in the aur
so we can install it with ea so we can
type in here yay
and then time shift and then hit enter
and you're going to have to basically
choose here one of the options now you
can see we have several here the time
shift bin is basically the binary for
time shift it's marked out of date so
i'm not gonna install it for now
then we have time shift auto snap so
this is basically a time shift auto
snapshot script which runs before
package upgrade using the pacman hook so
what this basically does is to create a
snapshot every time the system has
updates it's not going to create a
snapshot when you're installing new
packages for that you will need to
create manual snapshots but if you're
having updates in your system it's going
to take a snapshot before the update
so i'm going to install actually both by
typing in one and two separated by the
comma and then hit enter
now it's asking us whether we want to
remove the make dependencies after
install this is really up to you in my
case i'm going to say yes just to clean
up the packages that might not be any
more used afterwards
now differences to show here i don't
need them so i'm just typing no and then
hit enter
and now i can proceed with the
installation of the dependencies and
then we are going to build the packages
and install them
so depending also on your computer and
how fast it is it's going to take maybe
some time especially time shift it's
quite a big binary to build so i'm gonna
pause the video here guys and i'll be
back with you when it's done
so the packages have been installed and
i noticed during the installation of
time shift that there was a warning or
better said notice that you could
install also the grub butterfs package
in order to have snapshots appearing on
the grub bootloader
now this is not strictly necessary
because timeshift has anywhere the
option to restore snapshots so it's
really up to you but i'm going to
install it here nevertheless for
demonstration purpose so i'm going to
type in here sudo pacman
dash s and then grab
dash bada fs and then hit enter
and i'm going to proceed with the
installation
now it's going to rebuild here the
initrum fs
and that means basically every time
there is
an update on the system the snapshot is
going to appear also in the grub
bootloader now grub is not going to show
you snapshots that you took manually in
timeshift unless you rerun the grub
configuration file i'm going to show you
this afterwards so now we have the
packages installed let's close the
terminal here
and let's pull up time shift
so we need to authenticate so let's type
in the password
and we need to go through the setup here
so the file system is butterfs now the
disk this is the only disk i have and
this is actually the disk where butterfs
is so i'm going to select it and click
next
and this is the schedule so the schedule
right now it's fine i'm going to keep
the defaults here but you can change of
course as needed
now enable button fsq groups this is
recommended so i'm going to leave it so
i'm not gonna back up the home
directories and also here a word of
caution time shift is actually meant to
backup system files
we can click next and the setup is now
complete so we can click finish
so you can see here we have time shift
is active we don't have any snapshots
and this is the space available
so if i take a snapshot now by clicking
create
it's going to take basically a photo an
instant photo of the system right now so
i can close this up
and i can open up again the terminal and
let me again go full screen here and
increase the font size and let's for
example install something let's type in
here sudo
pacman dash s and let's install chromium
which is not installed by default here
in enable os
so we need to authenticate
and let's install the package it's going
to take a second to do this
but you can see here we have basically
nothing saying that the snapshot was
created or something similar and that's
because the auto snap feature as i said
before it's going to create snapshots
only when you are updating the system
and there are updates for your system
but when you are installing something if
you want to have a snapshot then you
will have to take it manually and if you
want to have those snapshots appearing
helping grub you will have to run the
grub configuration command again here in
the terminal so for example if i type in
now sudo and then grab
mk config
dash o slash boot slash grub slash grub
dot cfg
you will see we will have a line where
it's going to tell us that a snapshot
has been added to the graph bootloader
you can see it down here now you can of
course reboot the machine and boot into
the snapshots if you want but that
snapshot is going to be read only so
it's up to you as i said before it's not
really necessary to install grub
butterfest but if you want to do this
this is how you can do it now let's
reboot once the machine i just want to
show you there how it looks like it's
going to take a moment to do that
so here you can see we have endeavor os
this is the grub bootloader and we have
here a new option and there were os
snapshots if we hit enter here we'll
have the snapshot i created before i
installed chromium so if i hit enter
here we will have two images one is the
fallback and one is the linux image
which is the usual image you would put
in now you can boot from here and if you
do so timesheet will tell you that you
can actually restore the snapshot if you
click the restore option in time shift
so i'm not going to do this right now
i'm going to go back here and go back to
endeavor os and hit the first option
here to start the system normally
and let me enter my password here going
to go back in gnome and so let's put up
again time shift one more time
and hit my password here
and we have the snapshot that we created
before we installed chromium so what we
can do here we can actually click the
snapshot and click restore
so we have a warning here what will be
restored on which mount point which is
fine so we can click next
and the restore is completed now
restores of volumes will become active
after system is restarted
so let's go ahead and check that out so
let's close this
close time shift and
reboot our machine one more time
so you can see here we have back to
square one we don't have any more the
snapshot menu here because we restored
this before it was created and let's put
up the machine here and we shouldn't
have chromium as well
so let's enter the password here
and let me search for chromium and you
can see we don't have it so we are back
basically to the installation we had
before we installed chromium so let's
here hit one more time time shift
and these are the snapshots we have in
our time shift here so we have the one i
created manually and then we have the
one which was created before restoring
the previous snapshot
so if you don't need those snapshots now
anymore you can delete them if you want
to of course you can also browse them i
have also a video on time shift that you
can check out on the channel if you want
more information about time shift but
it's a very simple utility and here in
endeavor os is pretty simple to
integrate it other than that i'm really
enjoying endeavor os here the new iso i
will do another video for endeavor os
new iso here so stay tuned for that and
if you have any question about this
video let me know in the comments below
so that's it guys it's pretty simple to
install time shift on endeavor os if you
have any question let me know in the
comments below i will try to answer you
as soon as i can i wish you a great day
and i'll see you very soon in the next
video
