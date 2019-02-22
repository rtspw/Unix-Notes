# 1 - The Linux System: The Kernel

<br>

The **kernel** controls hardware allocation and software execution. 

Its main functions include:
- System Memory Management
- Software Program Management
- Hardware Management
- Filesystem Management

<br>

## System Memory Management

### Virtual Memory

The kernel manages both physical and virtual memory. 

Virtual memory doesn't exist. Space is used in the hard drive called a **swap space**. Groups of memory locations called **pages** are swapped between physical memory and disk.

When pages are not in use after a while, it is swapped out. When a page is needed, it is then swapped into memory.

<br>

## Software Program Management

### Processes

Any running program on linux is called a **process**.
They can run in the foreground rendering graphics, or manage background logic.

#### Initial Process

On bootup, the kernel loads the **init process** into virtual memory. 
Some distros use a table of processes to start, or scripts for starting all other processes. (These files are found in the `/etc` directory)

##### Init Levels

The Linux OS can start up in different levels of initialization, changing what processes are started.

| Init Level | Processes |
|---|---|
|1|'Single-user Mode': Basic terminal for emergencies and maintenance|
|3|Application and network software|
|5|Includes windows graphics processes|


<br>

## Hardware Management

For a hardware device to communicate with the kernel, the kernel needs **driver code**. 

Driver code used to require a complete recompilation of the kernel, but now it can be added modularly.

Classification of these files include:
- **Character**
  For devices that handle one character long buffers
- **Block**
  For devices that handle blocks of data, such as hard drives
- **Network**
  For devices that send and recieves packets, such as network cards
  
The OS creates **nodes**, which are interfaces to communicate between the hardware and the software.


<br>

## Filesystem Management

The kernel supports many filesystems to know how to read and write from the hard drive. This includes several including `ext`, `ntfs`, and so on.

It uses an interface, called the **Virtual File System (VFS)**, between the kernal and filesystem.
















