---
layout: wiki
title: Useful Linux/Unix commands
categories: Linux, Unix, Ubuntu
description: Useful linux/unix commands
keywords: Linux, Unix, Ubuntu
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
