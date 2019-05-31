# lfcs-study

## Basic Commands

### Files and Directories
#### du
    du file && du folder && du *
The 'du' command outputs the disk space occupied by files and folders.
    du -h file
The '-h' option makes the output human readable.
#### ls
    ls && ls directory
The 'ls' command outputs the content of a folder.

    $ ls -l
    total 2097256
    drwxr-xr-x   2 root root       4096 May 11 08:39 bin
    drwxr-xr-x   4 root root       4096 May 11 08:41 boot
    drwxr-xr-x   2 root root       4096 Jan 20 21:07 cdrom
    drwxr-xr-x  21 root root       4780 May 14 14:27 dev
    drwxr-xr-x 150 root root      12288 May 11 08:43 etc
    drwxr-xr-x   3 root root       4096 Jan 20 21:11 home
    . . .
The '-l' option requests output in long form.
#### tree
    tree
From the man page:
> "Tree is a recursive directory listing program that produces a depth indented listing of files..."
#### pwd
    pwd
From the man page:
> "Print the full filename of the current working directory."
#### touch
    touch -a foo
Updates the modification time of a file, creating it if it doesn't already exist.
#### mkdir
    mkdir foo
Creates the new directory 'foo'.
#### rmdir
    rmdir foo
Removes the empty directory, 'foo'. For a directory that isn't empty, use 'rm -r foo'.
#### mv
    mv foo ../bar/foo
Moves the file or folder, 'foo', a directory back and into the folder 'bar'.

    mv foo bar
Renames the file or folder, 'foo', to 'bar'.
#### cp
    cp foo bar
Creates a copy of the file or folder, 'foo', naming it 'bar'.
#### rm
    rm foo
Removes the file 'foo'.

    rm -r foo
Recursively removes the folder 'foo'. Used primarily for non-empty directories. For empty directories, use 'rmdir foo'.
 
### Standard File Permissions
#### Octal
Consists of a three digit number sequence describing the read, write and execute permissions that a group has on a file/folder.
Each digit is the sum of the following:
 - 1: Exec
 - 2: Write
 - 4: Read

The first digit notes the privileges for the owner, the second for the group and the third is for everyone else. Therefore, `chmod 764 foo` would alter permissions of foo so that the owner has all privileges, group has read and write, and everyone else can just read.

#### Absolute


#### Relative
#### Advanced Permissions

### Locate Files & Patterns
#### find
Recursive by default.
Examples:
 - `find /var/log -name '*.log'` searches for files with the '.log' suffix in /var/log.
 - `find /var/log -iname '*.log'` is the same but ignores case.
 - `find ~ -perm 777 -exec rm {} \;` searches files with 777 permissions and executes `rm {file}`. The 'exec' command must lie between '-exec' and the terminating '\\;'.
 - `find /etc -size -100k` searches for files in /etc that are smaller than 100 kilobytes. Likewise, `+100k` could be substituted to look for files greater than 100 kilobytes or `100k` for files exactly that size.
 - `find . -type f -size +2M -maxdepth 2` searches for only files greater than 2 megabytes at a maximum depth of 2 directory levels.
 - `find . \! -user owner` looks for files that are not owned by `'owner'`. The `'!'` operator negates and `'\'` escapes so that it can be interpreted by  the shell.
 - `find . -perm -222` finds files with at least write permissions for all. For example, this will return files with `222` and `777` but not `644` or `700`.
#### grep
Search for the pattern in a file or all files in a directory. Examples:
 - `grep -Rl` : Recursively (include symbolic links) list all files.
 - `grep -rl` : Recursively (do not include symbolic links) list all files.
 - `grep -RHn` : Search recursively (including symbolic links) for the word (output including path to file, line number and matching line)
 
### Compare & Manipulating Text
#### cmp
#### comm
#### diff
#### uniq
#### sort
#### sed
#### cut
#### tr
#### vi, vim

### Displaying Text
#### cat
#### less
#### more
#### head
#### tail
 
### Hard & Soft Links
#### ln, ln -s
 
### Regular Expressions
#### File Globbing
#### Regex
| Character |                Definition                |  Example   |        Result         |
| :-------: | :--------------------------------------: | :--------: | :-------------------: |
|     ^     |            Start of a string             |    ^abc    |    abc, abcd, abc1    |
|     $     |             End of a string              |    abc$    |  abc, rasabc, 2aabc   |
|     .     |       Any character except newline       |    a.c     |     abc, acc, a1c     |
|           |                                          | Alteration |           a           |
|   {...}   | Explicit quantity of preceding character |   ab{2}c   |         abbc          |
|   [...]   |   Explicit set of characters to match    |   a[bB]c   |        abc,aBc        |
| [a-z0-9]  |   One lower case characters or number    | a[a-z0-9]c |        aac,a1c        |
|   (...)   |           Group of characters            |  (abc){2}  |        abcabc         |
|     *     | Null or more of the preceding characters |    a*bc    | bc, abc, aabc, aaaabc |
|     +     |  One or more of the preceding character  |    a+bc    |       abc, aabc       |
|     ?     |  Null or one of the preceding character  |    a?bc    |        bc, abc        |
|    ^$     |               Empty string               |            |                       |

* Not all regular expressions are supported by `grep`. As alternative can be used `egrep`
#### Sed
 
### Redirection
#### < : redirect stdin
#### \> and >> : redirect stdout
#### 2> : redirect stderr
#### | : the stdout is transformed in stdin
#### |& : stderr to stdin
#### 2>&1 : redirect stderr to same place of stdout
 
### Users, Groups and Their Privileges
For privileges relating specifically to files, see
#### adduser
`adduser alex`
#### deluser
`deluser alex`
#### passwd
`passwd alex`
#### groups
`groups alex`
#### groupadd
`groupadd sudoadmins`
#### usermod
`usermod -aG sudoadmins alex`
#### groupdel
`groupdel sudoadmins`
#### visudo

## Service Configuration
### Configure a caching DNS server & maintain a DNS zone
### Configure email aliases
### Configure SSH servers and clients
### Configure an HTTP server
#### Configure HTTP server log files
#### Restrict access to a web page
#### Restrict access to the HTTP proxy server
### Configure an IMAP and IMAPS service
### Query and modify the behavior of system services at various operating modes
### Configure a database server
### Manage and configure containers
### Manage and configure Virtual Machines
https://computingforgeeks.com/virsh-commands-cheatsheet/
#### Install QEMU and KVM
First check the cpu to see whether or not it is capable of virtualization with the `kvm-ok` tool.

    $ sudo apt install cpu-checker
    $ kvm-ok
The following output tells us that the system is ready to virtualize.

    INFO: /dev/kvm exists
    KVM acceleration can be used
Once we have confirmed that the system is compatible, we can install the neccesary packages.

    $ sudo apt install qemu-kvm libvirt virt-install
Use `systemctl status libvirtd` to determine whether you need to start or enable the service, if neccesary.
#### Virsh Manage Storage Pools
List all existing pools.

    $ virsh pool-list --all
     Name                 State      Autostart
    -------------------------------------------
     default              active     yes

Create a new disk based pool

    $ sudo virsh pool-define-as vdisk1 dir - - - - "/home/alex/pools"
    Pool vdisk1 defined
    
    $ sudo virsh pool-build vdisk1
    Pool vdisk1 built
    
    $ sudo virsh pool-start vdisk1
    Pool vdisk1 started
    
    $ sudo virsh pool-autostart vdisk1
    Pool vdisk1 marked as autostarted
    
    $ virsh pool-list --all
     Name                 State      Autostart
    -------------------------------------------
     default              active     yes
     vdisk1               active     yes
     
    $ sudo cat /etc/libvirt/storage/vdisk1.xml
    <!--
    WARNING: THIS IS AN AUTO-GENERATED FILE. CHANGES TO IT ARE LIKELY TO BE
    OVERWRITTEN AND LOST. Changes to this xml configuration should be made using:
      virsh pool-edit vdisk1
    or other application using the libvirt API.
    -->
    
    <pool type='dir'>
      <name>vdisk1</name>
      <uuid>7b4ebbc0-1ec5-4f74-a83a-7fbb820d5da7</uuid>
      <capacity unit='bytes'>0</capacity>
      <allocation unit='bytes'>0</allocation>
      <available unit='bytes'>0</available>
      <source>
      </source>
      <target>
        <path>/home/alex/pools</path>
      </target>
    </pool>

#### Virsh Manage Volumes (Virtual Storage, within a pool)

    # Create a volume within the default pool.
    $ sudo virsh vol-create-as default  volume.qcow2  2G
    Vol test_vol2.qcow2 created
    $ ls /var/lib/libvirt/images
    volume.qcow2

#### Creating a New VM
##### newvm.sh
    #!/bin/bash
    #Alexander Woyte, May 2019
    #Usage: ./newvm.sh <name> <path to storage vol>
    sudo virt-install --name $1 \
        --ram 1024 --vcpus 1 \
        --os-type linux \
        --network network:default \
        --graphics none --console pty,target_type=serial \
        --location 'http://us.archive.ubuntu.com/ubuntu/dists/bionic/main/installer-amd64/' \
        --extra-args 'console=ttyS0,115200n8 serial' --force --debug \
        --disk $2,bus=virtio
  
Remember to `chmod +x newvm.sh`, adding executable permission to the current user.
This script will capture the prompt, so be prepared. Detatch from it with `^]`
Use the script, replacing arguments, like so:

    ./installvm.sh testvm0 /var/lib/libvirt/images/vol.qcow2
    
If you installed it with SSH, which you should've, move on to the next section about connecting to the machine.

#### Connecting to the New VM (SSH)
Find the IP address of the machine you need with the following:

    sudo virsh net-dhcp-leases default

`default` represents the default connection. Find your other connections with the following, which may not be neccesary:

    sudo virsh net-list
    
Alternatively, you may use the name of the vm to get IP and MAC info with the following:

    sudo virsh domifaddr testvm0
    
Lastly, connect to it:

    ssh alex@192.168.122.92

#### General VM Management
    sudo virsh list --all
This lists all of the virtual machines configured on the system. Taking away `--all` would only show running guests.

    sudo virsh start vm0
This starts a VM called `vm0`, which can also be referenced by its ID instead of name.

    sudo virsh autostart vm0
    sudo virsh autostart --disable vm0
Either enables or disables automatic start on host system boot. Only effective if service `libvirtd` is enabled to start on boot as well.

    sudo virsh shutdown vm0
This shuts down the guest.

    sudo virsh destroy vm0
This forcefully shuts down a VM, be careful.

    sudo virsh undefine vm0
This removes a VM from the system.

    sudo virsh console vm0
Enter a console on the system. Only works if the VM has been configured to use console.

##### Cloning Virtual Machines
First, pause or shutdown the system safely.

    sudo virsh suspend vm0
    # OR
    sudo virsh shutdown vm0

Use `sudo virsh list --all` to make sure that this was done effectively.

    sudo virt-clone --original vm0 --auto-clone

This command will create `vm0-clone`, however host name and DHCP configuration changes will need to be done in order to use them as separate networking devices.

As of right now, without starting `vm0-clone`, you will not find a recorded address for it. So, start it. Resume the original as well, if neccesary, but only after starting the clone. The clone will take on the network configuration of the original, and the original will cease to network, for now.

    sudo virsh start vm0-clone

If doing an address check with `domifaddr` returns blank results now, rather than errors, try again in a minute. There should be no more entries here, however, the address previously representing the original VM will now represent the clone, so ssh to the clone and make the following changes:

    $ sudo virsh domifaddr testvm0-clone
     Name       MAC address          Protocol     Address
    -------------------------------------------------------------------------------
     vnet0      52:54:00:78:a7:b3    ipv4         192.168.122.185/24
    $ ssh user@192.168.122.185
    # Shell Change
    $ sudo su
    $ echo "newhostname" > /etc/hostname
    $ sed -i "s/ubuntu/clonesys/g" /etc/hosts
