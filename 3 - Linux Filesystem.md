# 3 - Linux Filesystem

<br>

In Linux, file directories are denoted using the forward slash `/`.

<br>

## Virtual Directory

Unlike Windows, Linux does not use drives letters (such as C:) to denote physical drives.

Rather, all files are stored in the **virtual directory**, where all files branch from a single base **root** directory.

#### Mounting Drives

To incorporate another drive (hard drive, flash drive, etc.), it is mounted directly to the filesystem. 

<br>

![8677b131.png](:storage\b3d10c54-8bfd-4da7-a4c9-78fd8def52f2\8677b131.png)

<br>

#### Filesystem Hierarchy Standard (FHS)

The **FHS** is a standard naming system by with the root directories follow.

| Directory Name | Meaning | Purpose |
|---|---|---|
|/bin|Binary|GNU user utilities|
|/boot|Boot|Boot files|
|/dev|Device|Device node files|
|/etc|Etcetera|Configuration files|
|/home|Home|User directories (documents, etc.)|
|/lib|Library|Application Library files|
|/media|Media|Mount point for removable drives|
|/mnt|Mount|Mount point for removable drives|
|/opt|Optional|Third-party software and data|
|/proc|Process|Hardware and process info|
|/sbin|System Binary|GNU admin utilities|
|/run|Run|System runtime data|
|/srv|Service|Where local services store files|
|/sys|System|Hardware info files|
|/tmp|Temporary|Files created and destroyed|
|/usr|User Binary|User utilities and data|
|/var|Variable|Log files and others|

<br>

## Navigation

To traverse directories, use the `cd` command.

```bash
$ cd [destination]
```

If no destination is specified, you will go to the `/home` directory.


#### Absolute References

The absolute reference starts with `/`, refering to the root, such as:
```bash
$ cd /usr/bin
```

Doing just `cd /` will take you to the root directory.

#### Relative References

Relative references can start with nothing, and just refer to a file or directory in the current directory.

```bash
$ cd filename
```

There is also characters to represent relative paths:
- (.) for the current directory
- (..) for the parent directory

To go back up one level, we can use:
```bash
$ cd ../
```

#### Present Working Directory

The command `pwd` will print the current directory path.

```bash
/home$ pwd
/home
```





