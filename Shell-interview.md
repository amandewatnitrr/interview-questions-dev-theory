# Shell Interview Questions

### What is `chroot jail`?

- This scenario happens when Operating System doesnot allow a process running to access the parent directory.
- It is a way to isolate a process and its children from the rest of the system.
- It is used to :

  - create a sandbox environment for a process
  - run untrusted programs or services
  - test new software

- Example:

  ```bash
  chroot /path/to/new/root /path/to/new/root/bin/bash
  ```

  here `/path/to/new/root` is the new root directory, and `/path/to/new/root/bin/bash` is the new shell.

### What is shell scripting?

- A shell script is a text file containing a sequence of commands that are executed by the shell interpreter.
- It allows automation of repetitive tasks and execution of multiple commands in sequence.

### What is the difference between a shell and a terminal?

- Shell is a command-line interpreter that interprets the commands entered by the user and executes them.
- Terminal is a UI that provides an interface to interact with the shell.

### What is difference between shell and kernel?

- Shell is a command-line interpreter that interprets the commands entered by the user and executes them.
- Kernel is the core of the operating system that manages system resources and provides an interface for user-level processes to interact with hardware.

### What are subshells in shell scripting?

- A subshell is a child process created by the shell to execute a sequence of commands.
- It is used to isolate a group of commands from the parent shell.
- Example:

  ```bash
  > (command1; command2)
  # Example
  > (cd /path/to/directory; ls -a)
  ```

### Difference with Absolute and Relative path

- Absolute Paths: It starts from the root directory and specifies the full path to the file or directory.

  - Example:

    ```bash
    /home/user/file.txt
    ```

- Relative Paths: It specifies the path to the file or directory relative to the current working directory.

  - Example:

    ```bash
    ./user/file.txt
    ```

### What is the `shebang (#!)` line in a shell script ?

- `shebang line` (`#!`) is a special line at the beginning of a shell script that indicates the path to the shell interpreter that should be used to execute the script.

- For example,

  - `#!/bin/bash` specifies that the Bash shell should be used.
  - `#!/usr/bin/env python3` specifies that the Python 3 interpreter should be used.
  - `#!/usr/bin/perl` specifies that the perl interpreter should be used.

### What is the difference between $ and $$ in shell scripting ??

- `$` is used to access the value of a variable.
- `$$` is used to access the process ID of the current shell.

- Example:

  ```bash
  echo $HOME
  echo $$
  ```

### Count the number of files and directories in a directory

- To count the number of files and directories in a directory, you can use the following command:

  ```bash
  ls -1A | wc -l
  ```

  Here,

  - `-1` lists one file per line.
  - `-A` lists all files except `.` and `..`.
  - `wc -l` counts the number of lines.

- If we want to count the number of files only, we can use the following command:

  ```bash
  find . -type f | wc -l
  ```

  Here,

  - `. -type f` finds all files in the current directory.
  - `wc -l` counts the number of lines.

- If we want to count the number of directories only, we can use the following command:

  ```bash
  find . -type d | wc -l
  ```

  Here,

  - `. -type d` finds all directories in the current directory.
  - `wc -l` counts the number of lines.

### Explain the difference between the `&&` and `||` operators in shell scripting

- `&&` is a logical AND operator that executes the second command only if the first command is successful (returns 0).
- `||` is a logical OR operator that executes the second command only if the first command fails (returns non-zero).

- Example:

  ```bash
  command1 && command2
  command1 || command2
  ```

### What is process substitution in shell scripting ?

- Process substitution is a feature in bash that allows a process's output to be feed as input to another command or process.
- Example:

  ```bash
  diff <(ls dir1) <(ls dir2)
  ```

### Explain `grep` command in shell scripting

- `grep` command is used to search for patterns in text files or streams.
- Example:

  ```bash
  grep "pattern" file.txt # print all the lines in file.txt that contain "pattern"
  grep -i "error" logfile.txt # ignore case while searching for "error" in logfile.txt
  grep -w "error" logfile.txt # search for the exact whole word "error" in logfile.txt
  grep -c "error" logfile.txt # count the number of lines containing "error" in logfile.txt
  grep -r "error" /path/to/directory # search for "error" recursively in all files in the directory
  ```

### Explain `tar` command in shell scripting

- `tar` command is used to create, view, and extract tar archives.
- Example:

  ```bash
  tar -cvf archive.tar file1 file2 # create a tar archive
  tar -xvf archive.tar # extract a tar archive
  tar -tvf archive.tar # list the contents of a tar archive
  tar -cvzf archive.tar.gz . # create a gzip compressed tar archive
  ```

### What is SSH, and how it is used in Linux ?? How to generate SSH keys, and how to assign IP to SSH into a VM or a server ??

- SSH (Secure Shell) is a cryptographic network protocol used for secure remote access to Linux systems.
- provides encrypted communication between the client and the server, allowing users to log in and execute commands on remote machines securely

### How do you check system resource usage in Linux ?

- System resource usage can be checked using commands such as `top`, `htop`, `free`, and `df`
- `top` command displays real-time information about system processes and resource usage.
- `htop` is an interactive process viewer that provides a more user-friendly interface than `top`.
- `df` command displays disk space usage.

### What is `cron` ??

- `cron` is a time-based job scheduler in Unix-based operating systems.
- Example:

  ```bash
  crontab -e # edit the crontab file
  >  m h * * * /path/to/your/script.sh # run the script.sh specified hour every day, evry week for every month for every year
  crontab -l # list the crontab entries
  crontab -r # remove the crontab file
  ```

  - `cron.deny` and `cron.allow` are two files in the `/etc/cron.d` directory that controls access to the crontab command. 
  - Crontab command tasks such as creating, editing, displaying, or removing crontab files are relegated to specific users through these files
  - Both files usually consist of a list of user names, one user name per line. 
  - Together, these access control files perform the following functions:

  - cron.allow decides which users are allowed to run the crontab command.
  - cron.deny decides which users are denied from using the crontab command.
  - When `cron.allow` or `cron.deny` doesn't exist, superuser privileges are required to run it.


### `for loop` in shell scripting

- `for loop` is used to iterate over a list of items and perform a set of commands for each item.
- Example:

  ```bash
  for i in "${ar[@]}"
  do    
      echo $i
  done
  ```

### Shell Script to print process ID of a all running processes

- ```bash
  ps -eo pid,cmd
  ```

### Hard Link and Soft Link in Linux

- Hard Link:

  - A hard link is a direct pointer to the file's inode, which contains the file's metadata and data.
  - cannot be created for directories.
  - cannot span across file systems.
  - changes made to the original file are reflected in the hard link.
  - Example:

    ```bash
    ln file1 file2
    ```

- Soft Link:

  - A soft link is a pointer to the file's path, which contains the path to the file.
  - Also, known as `symbolic link`.
  - Soft links can span across different filesystems.
  - Deleting the original file or directory won’t affect the soft link; it will become a “dangling” link pointing to nothing.
  - Example:

    ```bash
    ln -s file1 file2
    ```

### How can we run a shell script in the background?

- To run a shell script in the background, append an `&` at the end of the command.

  ```bash
  ./script.sh &
  ```

### What is the use of the `$?` command?

- By using the command `$?`, you can find out the status of the last command executed.

### How to use pipe commands?

- Pipe commands are used to pass the output of one command as input to another command.

  ```bash
  command1 | command2 # output of command1 is passed as input to command2
  ```

### What is the use of `$!` ??

- `$!` is used to get the process ID of the last command executed in the background.

### Difference b/w `grep`, `find` and `sed` commands

- `grep` is used to search for patterns in text files or streams.
- `find` is used to search for files and directories based on various criteria.
- `sed` is used to perform text transformations on an input stream.

    ```bash
    find –type  f # Command will find all the files
    find  –type  d # Command will find all the directories
    find .  –name file1.txt # Command will find file1.txt in the current directory.
    ```

### How to open a read-only file in vi editor?

- To open a file in read-only mode in vi editor, use the following command:

  ```bash
  vi -R filename
  ```

# Storage Terminology and Concepts in Linux

### What is Block Storage ??

- `Block Storage` is another name what linux kernel calls as a `block device`.
- `Block Device` is a piece of hardware used to sotre data, more like a traditional hard drive.
- It is called `Block Device` because the kernel interfaces with the hardware by referencing fixed-size blocks.

### What are disk partitions ??

- When partitioning a disk, it is important to know what partitioning format is used. This generally comes down to choice b/w MBR and GPT.
- MBR being old, and having space limitations including the fact it can have at max only 4 partitions, GPT is the new standard.

### Formatting and File Systems

- `Formatting` is the process of writting a filesystem to a disk, and preparing it for operations.
- A `File System` is a system that structures data and how information is written to or read from the underlying disk.

### Popular File Systems

- `Ext4`

  - Succesor of `Ext3` and `Ext2`.
  - journaled, and backwards compatible with legacy systems.
  - Good choice, if there's no specialised needs

- `XFS`

  - Specializes in performance, and large data files.
  - formats quickly, and has good throughput for large files.
  - uses metadata journaling, instead of full journaling.
  - fast performance, but can lead to data loss in case of power failure.

- `Btrfs`

  - modern, feature-rich and copy-on-write filesystem.
  - allows for volume management functionality.
  - Used by default on some Network Attached Storage (NAS) devices.

- `ZFS`

  - copy-on-write filesystem, and volume manager.
  - Data Integrity features, and supports snapshots and clones.
  - Can organize volume into RAID arrays, for redundancy and performance purposes.

### How Linux manages storage devices

- In Linux, everything is represented by a file somewhere in the filesystem hierarchy.
- The storage devices are represented as files in the `/dev` directory either using the keyword `sd` or `hd` followed by a letter representing the device.
- For example, the first hard disk is represented as `/dev/sda`, and its partitions are represented as `/dev/sda1`, `/dev/sda2`, etc.

- While `/dev/sd*` and `/dev/hd*` are used to represent storage devices, there is a majore disadvantage to this approach.
- The Linux kernel decides which device gets which name on each boot, so this can lead to scenario where device changes device nodes.
- To solve this issue, the `/dev/disk/` directory contains more specific ways to identify disks and partitions on the system.

### Mounting

- `Mounting` is the process of attaching a drive to a directory in the filesystem.
- Drives are always mounted on dedicated empty directories
- We can mount a drive using the `mount` command.

  ```bash
  mount /dev/sdb1 /mnt
  ```

- We can make mounts permanent by adding them to the `/etc/fstab`  filesystem table file, which filesystems to mount at boot time.

  ```bash
  /dev/sdb1 /mnt ext4 defaults 0 0
  ```

  Filesytems that donot have entry in this file, will not be mounted automatically unless scripted by some one else, or some other software.

### RAID (Redundant Array of Independent Disks)

- RAID is a storage management and virtualization technology that allows us to group drives together and manage them as a single unit with additional capabilities.

  The characteristics of RAID depend on the level of RAID used, which define how disks in the array relate to each other.

  - `RAID 0` - Striping

    - Data is written in array, split up and distributed linearly among disks.
    - offers performance boost as multiple disks can be written to or read from simultaneously.
    - Single drive failure can lead to data loss in entire array.
    - As, no single disk contain all the data to rebuild the contents.
    - Therefore, never used in production for this reason.

  - `RAID 1` - Mirroring

    - Anything written to RAID 1 array is written to multiple disks.
    - Major issue is data redundancy, which kind of helps it in surrviving any data loss
    - Multiple drives contain the exact same data.

  - `RAID 5`

    - stripes data across multiple drives, similar to RAID 0.
    - implements distributed parity across all drives in the array.
    - This means if any one of the drives fail, it can be rebuild using the parity information stored on the other drives.
    - Reduces the available space by 1 disk

  - `RAID 10`

    - combination of levels 1 and 0
    - 2 set of mirriored arrays are made and data is stripped across them
    - Creates an array that has some data redundancy characteristics while providing good performance.
    - requires quite a few drives.

### How to view which process is using which port in Linux

- To view which process is using a specific port in Linux, you can use the `netstat` or `ss` command.

  ```bash
  netstat -tuln | grep :port_number
  # This will show the process ID and name of the process using the specified port.
  ss -tuln | grep :port_number
  # This will show the process ID and name of the process using the specified port.
  ```

  The Output would look something like this:

  ```bash
  Netid  State      Recv-Q Send-Q  Local Address:Port   Peer Address:Port  Process
  tcp    LISTEN     0      128     0.0.0.0:4000        0.0.0.0:*           users:(("nxserver.bin",pid=12345,fd=15))
  ```

  Here,

  - `-t` shows TCP ports.
  - `-u` shows UDP ports.
  - `-l` shows listening ports.
  - `-n` shows numerical addresses.
  - `-p` shows the process ID and name.