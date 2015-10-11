# Peter Piper Documentation

### 1. INTRODUCTION
<br>
This script was made as an alternative to legitimate authentication in Applescript. This script uses a method of exploitation in OS X called root piping.

<br>

### 2. EXPLOIT
<br>
This exploit uses a vulnerability that was properly fixed in OS X 10.10.5. It’s reference information is [here](https://www.sektioneins.de/en/blog/15-07-07-dyld_print_to_file_lpe.html).
This exploit gives whatever user that executes it admin instantly.

<br>

### 3. INSTALL
<br>
We use `cURL` to get the Java 8 Update 60 package onto the target computer and into a temporary directory, then the `installer` command featured in the OS X command line to install the .pkg we fetched. This is the correct command for this particular task because it skips the graphical installer meaning it can run behind the scenes without target knowledge.

<br>

### 4. CLEANUP
<br>
We first remove the temporary directory used to store the Java package during install, then we use the command `sed` to remove the target from the sudoers list.

<br>

### 5. `function KeepSafe { }` & `trap`
<br>
This is used to ensure the completion of the command if it fails.


### License
MIT License
