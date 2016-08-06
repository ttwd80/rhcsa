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
    [centos@localhost ~]$ echo two > /tmp/file.txt
    [centos@localhost ~]$ cat /tmp/file.txt
    two
    ```
