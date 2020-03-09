---
layout: wiki
title: Useful Linux/Unix commands
categories: Linux, Unix, Ubuntu
description: Useful linux/unix commands
keywords: Linux, Unix, Ubuntu
active: true
---

Useful linux/unix commands

### SCP (Secure Copy)

Command

```sh
$ scp source_file_path destination_file_path
```

The file path should include the full host address, port number, username and password

#### Copy a directory

```sh
$ scp -v -r ~/Downloads root@192.168.1.1:/root/Downloads
```

#### Transfer multiple files

```sh
$ scp foo.txt bar.txt username@remotehost:/path/directory/
```
or

```sh
$ scp username@remotehost:/path/directory/\{foo.txt,bar.txt\} .

$ scp root@192.168.1.3:~/\{abc.log,cde.txt\} .
```

#### Copy files across 2 remote hosts

```sh
$ scp user1@remotehost1:/some/remote/dir/foobar.txt user2@remotehost2:/some/remote/dir/
```

#### Speed up the transfer with compression

```sh
scp -vrC ~/Downloads root@192.168.1.3:/root/Downloads
```

### CP (Copy)

### MV (Move)

### Find

#### Search for all files in a specific directory

```sh
$ find /path/to/file/
```

or search files in the current directory

```sh
$ find .
```

To search for a file named e.g “softwares” under current directory

```sh
$ find . -iname filename
```

#### Search using a wildcard

```sh
$ find /path/to/file/ -iname filename*
```

#### Search based on date and time

mtime (Modification time): when the file’s content was modified last time.
atime (Access time): when the file was accessed last time.
ctime (Change time): when the file attributes were modified last time.

Search for files in a current directory that were modified less than 2 days ago

```sh
$ find . -mtime -2
```

Search for files that were accessed less than 2 days ago

```sh
$ find . –atime -2
```

Search for files that were changed less than 2 days ago

```sh
$ find . –ctime -2
```

#### Search based on file size

Search file whose size is larger than 5MB size

```sh
$ find . –size +5M\
```

#### Search based on file permissions

Find files with specific permission

```sh
$ find . –type f –perm 644
```



