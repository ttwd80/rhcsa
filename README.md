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
