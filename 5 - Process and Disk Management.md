# 5 - Process and Disk Management
<br>

We have already seen how to look at the processes at a point in time in [[0 - Basic Unix Commands]]

### Real-time Monitoring

The `top` command will show a real-time display of all running processes. 

```bash
top - 18:51:07 up 70 days,  1:09,  0 users,  load average: 2.23, 1.62, 1.56
Tasks:   9 total,   2 running,   7 sleeping,   0 stopped,   0 zombie
%Cpu(s):  6.2 us,  9.0 sy,  0.0 ni, 83.3 id,  0.0 wa,  0.0 hi,  1.5 si,  0.0 st
KiB Mem:  53595384 total, 49824380 used,  3771004 free,  6849380 buffers
KiB Swap: 52428796 total,   983212 used, 51445584 free. 29063192 cached Mem

    PID USER      PR  NI    VIRT    RES    SHR S  %CPU %MEM     TIME+ COMMAND                                       
    175 ubuntu    20   0 1243464  51616  15952 R   2.4  0.1   0:01.26 vfs-worker {"pi                               
      1 root      20   0    1104      4      0 S   0.0  0.0   0:00.04 tini                                          
      7 root      20   0    4052    192    152 S   0.0  0.0   0:00.00 micro-inetd                                   
    174 root      20   0   19376   2116   1924 S   0.0  0.0   0:00.17 dropbear                                      
   1071 ubuntu    20   0  123736   2708   2512 S   0.0  0.0   0:00.00 tmux                                          
   1074 ubuntu    20   0  132564   3568   2856 S   0.0  0.0   0:00.04 tmux                                          
   1075 ubuntu    20   0   11276   2676   2492 S   0.0  0.0   0:00.00 bash                                          
   1076 ubuntu    20   0   29124  12884   3172 S   0.0  0.0   0:00.23 bash                                          
   1563 ubuntu    20   0   23644   2736   2404 R   0.0  0.0   0:00.01 top     
```

- In the first row, we have current time, uptime, and load average for 1, 5, and 15 minutes.
- In the second row, we have task stats, where `zombie` refers to finished processes waiting for their parent to respond.
- In the third row, we have cpu statistics with the meanings:


| Term | Meaning | Purpose |
|---|---|---|
|us|user time|CPU time spent in user space|
|sy|system time| kernel space|
|ni|nice time| low priority processes |
|id|idle time| idling|
|wa|io wait time| wait on disk|
|hi|hardware irq|handling hardware interrupts|
|si|software irq|handling software interrupts|
|st|steal time|time used by processes other than the linux virutal machine|
   
- The last two rows show how much physical and swap memory is being used (for virtual memory)

<br>

### Process Signals

Most processes communicate and act using a set of standard process systems, which a well-written application would receive and act.

| Signal | Name | Meaning |
|---|---|---|
|1|HUP|Hang up|
|2|INT|Interrupt|
|3|QUIT|Quit|
|9|KILL|Terminates program without condition|
|11|SEGV|Segment Violation|
|15|TERM|Terminates with condition (if possible)|
|17|STOP|Stops without condition (not terminate)|
|18|TSTP|Stops but runs in background|
|19|CONT|Resume after STOP or TSTP|

<br>

#### $ kill

The `kill` command sends a `TERM` signal to a process using a Process ID (PID).

```bash
$ kill [options] [PID]
```

```bash
$ kill 1234
```

If the process is runaway, then it will likely not respond to `TERM`.
In such conditions, you can use other signals using the `-s` option.

```bash
$ kill -s HUP 1234
```

<br>

#### $ killall

The `killall` command can take a wildcard pattern and terminate all processes with that name.

```bash
$ killall http*
```

<br><br>

---

### Mounting

When external drives are plugged in, they must be mounted to the virtual directory.

Most distros automatically mount flash drives to `/media/disk/`. 

However, if that is not the case, it must be manually mounted with the `mount` command.

<br>

#### $ mount

The basic form is:
```bash
mount -t [media type] [device name] [directory]
```

Before mounting, the drives will be in the `/dev` folder. 

Some common media types include:
- **vfat**: Window's system for flash drives
- **ntfs**: Window's advanced file system
- **iso9660**: Commonly used for CDs

A full example of a mount:
```bash
mount -t vfat /dev/sdb1 /media/disk
```

<br>

#### $ umount

To unmount a drive, use the `umount` command (no n). 
```bash
umount [directory || device]
```
This allows for both the directory or device name.
For example:
```bash
umount /media/disk
```
or
```bash
umount /dev/sdb1
```

<br>

#### $ df

To view available disk space for each device, use the `df` command.

```bash
Filesystem                1K-blocks      Used Available Use% Mounted on
none                        2234668     51828   2047724   3% /
tmpfs                      26797692         0  26797692   0% /dev
tmpfs                      26797692         0  26797692   0% /sys/fs/cgroup
```

Instead of 1K-blocks, we can view with megabytes and gigabytes using the `-h` option.

```bash
Filesystem                1K-blocks      Used Available Use% Mounted on
none                      2.2G   51M  2.0G   3% /
tmpfs                      26G     0   26G   0% /dev
tmpfs                      26G     0   26G   0% /sys/fs/cgroup
```

<br>

#### $ du

The `du` command recursively displays all files from the current directory, along with the amount of disk blocks each directory uses. This can be used to find which directories are taking all the space.

Some common flags include `-c` to get a grand total, `-h` for human-readable (in k,m,g bytes), and `-s` for a summary.

For example (just a small part of the listing):
```bash
...
28K     ./Express/node_modules/etag
24K     ./Express/node_modules/encodeurl
44K     ./Express/node_modules/safe-buffer
20K     ./Express/node_modules/destroy
28K     ./Express/node_modules/merge-descriptors
24K     ./Express/node_modules/bytes
24K     ./Express/node_modules/range-parser
28K     ./Express/node_modules/finalhandler
64K     ./Express/node_modules/qs/test
36K     ./Express/node_modules/qs/lib
24K     ./Express/node_modules/qs/dist
180K    ./Express/node_modules/qs
12K     ./Express/node_modules/express/lib/middleware
32K     ./Express/node_modules/express/lib/router
124K    ./Express/node_modules/express/lib
260K    ./Express/node_modules/express
20K     ./Express/node_modules/raw-body/node_modules/setprototypeof
8.0K    ./Express/node_modules/raw-body/node_modules/depd/lib/browser
16K     ./Express/node_modules/raw-body/node_modules/depd/lib/compat
28K     ./Express/node_modules/raw-body/node_modules/depd/lib
...
```

<br><br>

--- 

### Working with Files

#### Sorting Files

The `sort` command takes in a filename and outputs a sorted version of it (line by line). 

It sorts alphabetically, so for cases such as numbers or months, other parameters must be used.
Some include:
- `-n` for numbers
- `-M` for three letter months
- `-f` ignores case
- `-r` print in reverse order
- `-u` ignore repeat lines

The parameters `-k` and `-t` can be used for sorting a certain column of character-separated lines, such as `csv`s, or comma-separated value sheets.

```bash
sort -t ',' -k 3 -n /example/csvfile
```

`-t` takes the character to delimit by, and `-k` takes the column number (which in this case, is a numerical column)

We can apply this command to the output of our previous command `du`:

```bash
exampleuser:~/workspace/Express/node_modules $ du -h | sort -nr
416K    ./iconv-lite
348K    ./iconv-lite/encodings
260K    ./express
232K    ./iconv-lite/encodings/tables
184K    ./mime-db
180K    ./qs
164K    ./raw-body
136K    ./ipaddr.js
124K    ./raw-body/node_modules
124K    ./express/lib
112K    ./debug
88K     ./body-parser
68K     ./raw-body/node_modules/depd
68K     ./mime
68K     ./depd
64K     ./qs/test
...
```

<br>

### File Compression

Compression is taking files and turning them into smaller files. Compressed files, as such, must be uncompressed first before they can be used.

Linux compression utilities include:
| Utility | File extension | Info |
|---|---|---|
|bzip2|.bz2|Burrows-Wheeler block sorting and Huffman coding|
|compress|.Z|Original Unix compression, no longer used|
|gzip|.gz|GNU's compression util using Lempel-Ziv coding. Most popular.|
|zip|.zip|Unix version of Window's style zip|

To `gzip` data, simply use the `gzip` command.
```bash
gzip [filename]
```

Note that the zipped file will replace the original.

- To view the gzipped file, use `gzcat`.
- To uncompressing the file, use `gunzip`.

For example:
```bash
exampleuser:~/documents $ ls
test
exampleuser:~/documents $ gzip test
exampleuser:~/documents $ ls
test.gz
```

You can also use wildcards to compress more than one file.

<br>

### File Archiving

Archiving is taking multiple files and turning it into one file. Usually on Windows, compression and archving is done in one step with zip. However, on Linux the process is separate. 

<br>

**To archive multiple files, we use the `tar` command. **
```bash
tar [command flag] -f [filename]...
```

**Parameter order matters!**. For example, `-f` must be followed by the filename. 
<br>

**To archive multiple files, we use the flags `-cf [output file] [file1] [file2] ...`.**
- `-c`: Create file (command flag)
- `-f`: Use file
- `-v`: Verboose mode
```bash
tar -cvf test.tar test1 testdirectory/
```

<br>

**To list the contents of a tar file, we can use the flags `-tf [tar file]`.**
- `-t`: List contents (command flag)
- `-f`: Use file
- `-v`: Verboose mode (optional) (similar to ls -l)

```bash
tar -tf test.tar
```

<br>

**To extract archived files to the current directory, use `-xf [tar file]`.**
- `-x`: Extract files (command flag)
- `-f`: Use file
- `-v`: Verboose mode

```bash
tar -xvf test.tar
```
<br>

A common file type is `.tar.gz` or `.tgz`. This is a tar file that has been gzipped.
For example using:
```bash
gzip test.tar
```
will give you `test.tar.gz`.

**To extract tar and gzipped files into the directory, use `-zxf [tar file]`.**
- `-z`: Redirect output to `gzip` utility
- `-x`: Extract files (command flag)
- `-f`: Use file
- `-v`: Verboose mode
```bash
tar -zxvf test.tar.gz
```

