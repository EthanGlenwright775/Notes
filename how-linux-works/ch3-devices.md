# 3 - Devices

## 3.1 - Device Files
* kernel presents many device I/O interfaces to user processes as files
* located in /dev directory
* `ls -l` - first character of file mode, b, c, p, and s indicate devices
    * `b` - block
    * `c` - character
    * `p` - pipe
    * `s` - socket
* Block device - programs access data from block device in fixed chunks
    * example, disks
    * total size fixed and easy to index
* Character device - work with data streams, can only read characters from or write characters to
    * example, /dev/null
    * does not have a size and data can only be read once
* Pipe device - named pipes are like character devices with another process at the other end of the I/O stream instead of a kernel driver
* Socket device - special purpose interfaces frequently used for interprocess communication, found outside /dev directory

## 3.2 - The sysfs Device Path
* `/sys/devices` - newer interface for devices
