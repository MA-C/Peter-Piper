# Peter Piper Documentation #

__1. INTRODUCTION__
<br>
This script was made as an alternative to legitimate authentication in Applescript. This script uses a method of exploitation in OS X  called root piping.

<br>

__2. EXPLOIT__
<br>
This exploit uses a vulnerability that was properly fixed in OS X 10.10.5. It’s reference information is https://www.sektioneins.de/en/blog/15-07-07-dyld_print_to_file_lpe.html
This exploit gives whatever user that executes it admin instantly.

<br>

__3. INSTALL__
<br>
We used `cURL` to get Java 8 Update 60 onto the target computer in a temporary directory. Then we used the `installer` bash command featured in the OS X command line to install the .pkg we fetched. This is the correct command for this particular task because it skips the graphical installer meaning it can run behind the scenes without target knowledge.

<br>

__4. CLEANUP__
<br>
We first remove the temporary directory used to store the Java package during install, then we use the bash command `sed` to remove the target from the sudoers list.

<br>

__5. `function KeepSafe {}` & `trap`__
<br>
This is used to ensure the completion of the command.
