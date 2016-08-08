# rhcsa

https://www.redhat.com/en/services/training/ex200-red-hat-certified-system-administrator-rhcsa-exam

Section 1: Understand and use essential tools
- Access a shell prompt and issue commands with correct syntax

  ```
  [centos@localhost ~]$ echo abc
  abc
  ```
- Use input-output redirection (>, >>, |, 2>, etc.)
  - Direct stdout

    ```
    [centos@localhost ~]$ echo one
    one
    ```
  - Redirect stdout using >

    ```
    [centos@localhost ~]$ rm -f /tmp/file.txt
    [centos@localhost ~]$ echo one > /tmp/file.txt
    [centos@localhost ~]$ cat /tmp/file.txt
    one
    ```
  - Redirect stdout using > (overwrite)

    ```
    [centos@localhost ~]$ rm -f /tmp/file.txt
    [centos@localhost ~]$ echo one > /tmp/file.txt
    [centos@localhost ~]$ echo two > /tmp/file.txt
    [centos@localhost ~]$ cat /tmp/file.txt
    two
    ```
  - Redirect stdout using >> (append)

    ```
    [centos@localhost ~]$ rm -f /tmp/file.txt
    [centos@localhost ~]$ echo one > /tmp/file.txt
    [centos@localhost ~]$ echo two >> /tmp/file.txt
    [centos@localhost ~]$ cat /tmp/file.txt 
    one
    two
    ```
  - Using pipes - |

    ```
    [centos@localhost ~]$ echo one > /tmp/file.txt 
    [centos@localhost ~]$ echo two >> /tmp/file.txt 
    [centos@localhost ~]$ grep wo /tmp/file.txt 
    two
    ```
  - Direct stderr

    ```
    [centos@localhost ~]$ asdasdf
    bash: asdasdf: command not found...
    ```
  - Redirect stderr using 2>

    ```
    [centos@localhost ~]$ asdasdf 2> /tmp/file.txt
    [centos@localhost ~]$ cat /tmp/file.txt 
    bash: asdasdf: command not found...
    ```
  - Redirect stdout to file and display stderr

    ```
    [centos@localhost ~]$ (echo one && asdfasdf) > /tmp/file.txt
    bash: asdfasdf: command not found...
    [centos@localhost ~]$ cat /tmp/file.txt 
    one
    ```
  - Display stdout and redirect stderr to file

    ```
    [centos@localhost ~]$ (echo one && asdfasdf) 2> /tmp/file.txt
    one
    [centos@localhost ~]$ cat /tmp/file.txt 
    bash: asdfasdf: command not found...
    ```
  - Display both stdout and stderr

    ```
    [centos@localhost ~]$ (echo one && asdfasdf)
    one
    bash: asdfasdf: command not found...
    ```
  - Redirect both stdout and stderr to file

    ```
    [centos@localhost ~]$ (echo one && asdfasdf) > /tmp/file.txt 2>&1
    [centos@localhost ~]$ cat /tmp/file.txt 
    one
    bash: asdfasdf: command not found...    
    ```

- Use grep and regular expressions to analyze text
  - Grep without regular expression

    ```
    [centos@localhost ~]$ rm -f /tmp/file.txt 
    [centos@localhost ~]$ for n in {1..100} ; do echo $n >> /tmp/file.txt ; done
    [centos@localhost ~]$ grep 6 /tmp/file.txt 
    6
    16
    26
    36
    46
    56
    60
    61
    62
    63
    64
    65
    66
    67
    68
    69
    76
    86
    96
    ```
  - Grep with regular expression
  
    ```
    [centos@localhost ~]$ rm -f /tmp/file.txt 
    [centos@localhost ~]$ for n in {1..100} ; do echo $n >> /tmp/file.txt ; done
    [centos@localhost ~]$ grep "6$" /tmp/file.txt 
    6
    16
    26
    36
    46
    56
    66
    76
    86
    96
    ```
- Access remote systems using ssh

  ```
    [centos@localhost ~]$ ssh localhost
    The authenticity of host 'localhost (::1)' can't be established.
    ECDSA key fingerprint is 36:89:50:3d:9c:01:6d:e1:59:35:cb:59:29:cb:a4:fc.
    Are you sure you want to continue connecting (yes/no)? yes
    Warning: Permanently added 'localhost' (ECDSA) to the list of known hosts.
    centos@localhost's password: 
    Last login: Sat Aug  6 17:28:12 2016 from 192.168.56.1
    [centos@localhost ~]$ 
  ```
- Log in and switch users in multiuser targets
  - Log in
  
  ```
    [root@localhost ~]# whoami 
    root
    [root@localhost ~]# ssh centos@localhost
    centos@localhost's password: 
    Last login: Sat Aug  6 19:28:42 2016 from localhost
    [centos@localhost ~]$ whoami 
    centos
  ```  
  - Switch user in multiuser targets
  
  ```
    [centos@localhost ~]$ whoami
    centos
    [centos@localhost ~]$ su -
    Password: 
    Last login: Sat Aug  6 17:14:58 AEST 2016 on pts/0
    [root@localhost ~]# whoami 
    root
  ```
- Archive, compress, unpack, and uncompress files using tar, star, gzip, and bzip2
  - Archive using tar
  
    ```
    [centos@localhost ~]$ rm -rf files
    [centos@localhost ~]$ mkdir files
    [centos@localhost ~]$ ls -1 files/
    [centos@localhost ~]$ date > files/file-1.txt
    [centos@localhost ~]$ date > files/file-2.txt
    [centos@localhost ~]$ date > files/file-3.txt
    [centos@localhost ~]$ ls -1 files/
    file-1.txt
    file-2.txt
    file-3.txt
    [centos@localhost ~]$ rm -rf files.tar
    [centos@localhost ~]$ tar cvf files.tar files/
    files/
    files/file-1.txt
    files/file-2.txt
    files/file-3.txt
    [centos@localhost ~]$ file files.tar 
    files.tar: POSIX tar archive (GNU)
    ```
  - Unpack archive using tar
  
    ```
    [centos@localhost ~]$ rm -rf files
    [centos@localhost ~]$ rm -rf files.tar
    [centos@localhost ~]$ mkdir files
    [centos@localhost ~]$ ls -1 files/
    [centos@localhost ~]$ date > files/file-1.txt
    [centos@localhost ~]$ date > files/file-2.txt
    [centos@localhost ~]$ date > files/file-3.txt
    [centos@localhost ~]$ ls -1 files/
    file-1.txt
    file-2.txt
    file-3.txt
    [centos@localhost ~]$ tar cvf files.tar files/
    files/
    files/file-1.txt
    files/file-2.txt
    files/file-3.txt
    [centos@localhost ~]$ rm -rf files/
    [centos@localhost ~]$ ls -1 files/
    ls: cannot access files/: No such file or directory
    [centos@localhost ~]$ tar xvf files.tar
    files/
    files/file-1.txt
    files/file-2.txt
    files/file-3.txt
    [centos@localhost ~]$ ls -1 files/
    file-1.txt
    file-2.txt
    file-3.txt
    ```
  - Archive using star 
  
    ```
    [centos@localhost ~]$ rm -rf files
    [centos@localhost ~]$ rm -rf files.star
    [centos@localhost ~]$ mkdir files
    [centos@localhost ~]$ ls -1 files/
    [centos@localhost ~]$ date > files/file-1.txt
    [centos@localhost ~]$ date > files/file-2.txt
    [centos@localhost ~]$ date > files/file-3.txt
    [centos@localhost ~]$ ls -1 files.star
    ls: cannot access files.star: No such file or directory
    [centos@localhost ~]$ star -c -f=files.star files/
    star: 1 blocks + 0 bytes (total of 10240 bytes = 10.00k).
    [centos@localhost ~]$ ls -1 files.star
    files.star
    ```
  - Unpack archive using star 
  
    ```
    [centos@localhost ~]$ rm -rf files
    [centos@localhost ~]$ rm -rf files.tar
    [centos@localhost ~]$ mkdir files
    [centos@localhost ~]$ ls -1 files/
    [centos@localhost ~]$ date > files/file-1.txt
    [centos@localhost ~]$ date > files/file-2.txt
    [centos@localhost ~]$ date > files/file-3.txt
    [centos@localhost ~]$ ls -1 files/
    file-1.txt
    file-2.txt
    file-3.txt
    [centos@localhost ~]$ star -c -f=files.star files/
    star: 1 blocks + 0 bytes (total of 10240 bytes = 10.00k).
    [centos@localhost ~]$ ls -1 files.star
    files.star
    [centos@localhost ~]$ rm -rf files/
    [centos@localhost ~]$ ls -1 files/
    ls: cannot access files/: No such file or directory
    [centos@localhost ~]$ star -x -f=files.star
    star: 1 blocks + 0 bytes (total of 10240 bytes = 10.00k).
    [centos@localhost ~]$ ls -1 files/
    file-1.txt
    file-2.txt
    file-3.txt
    ```
  - Compress using gzip
  
    ```
    [centos@localhost ~]$ rm -rf file*
    [centos@localhost ~]$ dd if=/dev/zero of=file bs=1M count=100
    100+0 records in
    100+0 records out
    104857600 bytes (105 MB) copied, 0.0474118 s, 2.2 GB/s
    [centos@localhost ~]$ ls -s file*
    102400 file
    [centos@localhost ~]$ gzip file
    [centos@localhost ~]$ ls -s file*
    100 file.gz
    ```
  - Uncompress using gzip
  
    ```
    [centos@localhost ~]$ rm -rf file*
    [centos@localhost ~]$ dd if=/dev/zero of=file bs=1M count=100
    100+0 records in
    100+0 records out
    104857600 bytes (105 MB) copied, 0.0482277 s, 2.2 GB/s
    [centos@localhost ~]$ ls -s file*
    102400 file
    [centos@localhost ~]$ gzip file
    [centos@localhost ~]$ ls -s file*
    100 file.gz
    [centos@localhost ~]$ gunzip file.gz 
    [centos@localhost ~]$ ls -s file*
    102400 file
    ```
- Create and edit text files

  ```
  [centos@localhost ~]$ vi file
  ```
- Create, delete, copy, and move files and directories
  - Create files
  
    ```
    [centos@localhost ~]$ rm -rf file*
    [centos@localhost ~]$ ls -1 file
    ls: cannot access file: No such file or directory
    [centos@localhost ~]$ touch file
    [centos@localhost ~]$ ls -1 file
    file
    ```
  - Delete files
  
    ```
    [centos@localhost ~]$ rm -rf file*
    [centos@localhost ~]$ ls -1 file
    ls: cannot access file: No such file or directory
    [centos@localhost ~]$ touch file
    [centos@localhost ~]$ ls -1 file
    file
    [centos@localhost ~]$ rm file
    [centos@localhost ~]$ ls -1 file
    ls: cannot access file: No such file or directory
    ```
  - Copy files
  
    ```
    [centos@localhost ~]$ rm -rf file*
    [centos@localhost ~]$ ls -1 file*
    ls: cannot access file*: No such file or directory
    [centos@localhost ~]$ dd if=/dev/zero of=file1 bs=1M count=10
    10+0 records in
    10+0 records out
    10485760 bytes (10 MB) copied, 0.00449607 s, 2.3 GB/s
    [centos@localhost ~]$ cp file1 file2
    [centos@localhost ~]$ ls -s file*
    10240 file1  10240 file2
    [centos@localhost ~]$ diff file1 file2
    ```
  - Move files
  
    ```
    [centos@localhost ~]$ rm -rf file*
    [centos@localhost ~]$ touch file-1.txt
    [centos@localhost ~]$ mkdir files
    [centos@localhost ~]$ ls -1 files/
    [centos@localhost ~]$ mv file-1.txt files
    [centos@localhost ~]$ ls -1 files/
    file-1.txt
    ```
- Create hard and soft links
  - Create hard links
  
    ```
    [centos@localhost ~]$ rm -rf file*
    [centos@localhost ~]$ touch file-1.txt
    [centos@localhost ~]$ ls -i file*
    104156772 file-1.txt
    [centos@localhost ~]$ ln file-1.txt file-2.txt
    [centos@localhost ~]$ ls -i file*
    104156772 file-1.txt  104156772 file-2.txt
    [centos@localhost ~]$ file file-1.txt
    file-1.txt: empty
    [centos@localhost ~]$ file file-2.txt
    file-2.txt: empty
    ```
  - Create soft links
  
    ```
    [centos@localhost ~]$ rm -rf file*
    [centos@localhost ~]$ touch file-1.txt
    [centos@localhost ~]$ ls -i file*
    104156772 file-1.txt
    [centos@localhost ~]$ ln -s file-1.txt file-2.txt
    [centos@localhost ~]$ ls -i file*
    104156772 file-1.txt  104156783 file-2.txt
    [centos@localhost ~]$ file file-1.txt
    file-1.txt: empty
    [centos@localhost ~]$ file file-2.txt
    file-2.txt: symbolic link to `file-1.txt'
    ```
- List, set, and change standard ugo/rwx permissions
  - List standard ugo/rwx permissions
  
    ```
    [centos@localhost ~]$ rm -rf file-1.txt
    [centos@localhost ~]$ touch file-1.txt
    [centos@localhost ~]$ ls -l file-1.txt | cut -f 1 -d' '
    -rw-rw-r--.
    ```
  - Set standard ugo/rwx permissions
  
    ```
    [centos@localhost ~]$ rm -rf file-1.txt
    [centos@localhost ~]$ touch file-1.txt
    [centos@localhost ~]$ ls -l file-1.txt | cut -f 1 -d' '
    -rw-rw-r--.
    [centos@localhost ~]$ chmod go= file-1.txt 
    [centos@localhost ~]$ ls -l file-1.txt | cut -f 1 -d' '
    -rw-------.
    ```
  - Change standard ugo/rwx permissions
  
    ```
    [centos@localhost ~]$ rm -rf file-1.txt
    [centos@localhost ~]$ touch file-1.txt
    [centos@localhost ~]$ ls -l file-1.txt | cut -f 1 -d' '
    -rw-rw-r--.
    [centos@localhost ~]$ chmod o+w file-1.txt 
    [centos@localhost ~]$ ls -l file-1.txt | cut -f 1 -d' '
    -rw-rw-rw-.
    ```
- Locate, read, and use system documentation including man, info, and files in /usr/share/doc
  
    ```
    [centos@localhost ~]$ man ls
    ```

Section 2: Operate running systems
- Boot, reboot, and shut down a system normally
  - Boot
  - Reboot now
  
    ```
    [root@localhost active]# shutdown -r now
    ```
  - Shutdown 
    
    ```
    [root@localhost active]# shutdown now
    ```
- Boot systems into different targets manually
    
    ```
    [root@localhost ~]# systemctl isolate multi-user.target 
    ```
- Interrupt the boot process in order to gain access to a system
  
  1. e to edit grub
  1. add 'rd.break enforcing=0' at the end of linux16
  1. control-x to start
  1. remount as read-write ```mount -o remount,rw /sysroot```
  1. confirm ```mount | grep /sysroot```
  1. ```chroot /sysroot```
  1. ```passwd```
  1. enter new password
  1. enter new password again
  1. ```exit```
  1. ```exit```
  1. ```restorecon /etc/shadow```
  1. ```reboot```
  
- Identify CPU/memory intensive processes, adjust process priority with renice, and kill processes  
  - Identify CPU/memory intensive processes
    
    Use ```top```
    
  - Adjust process priority with renice
    
    ```renice -n 10 pid```
    
  - kill processes
    
    ```kill pid```
- Locate and interpret system log files and journals
  
  x```journalctl```
- Access a virtual machine's console
- Start and stop virtual machines
- Start, stop, and check the status of network services
- Securely transfer files between systems
