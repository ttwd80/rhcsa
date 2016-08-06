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
  - Archive using tar 
