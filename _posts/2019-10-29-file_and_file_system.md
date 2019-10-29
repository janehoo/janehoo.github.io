---
title: Python刻意练习---Task07：文件与文件系统（2day）
categories:
 - deliberate-practice
tags:
 - python
---
## 文件
### 打开文件
使用`open()`打开一个文件

我们可以先执行`help(open)`看看详细文档,
```
open(file, mode='r', buffering=-1, encoding=None, errors=None, newline=None, closefd=True, opener=None)
    Open file and return a stream.  Raise OSError upon failure.
    
    file is either a text or byte string giving the name (and the path
    if the file isn't in the current working directory) of the file to
    be opened or an integer file descriptor of the file to be
    wrapped. (If a file descriptor is given, it is closed when the
    returned I/O object is closed, unless closefd is set to False.)
    
    mode is an optional string that specifies the mode in which the file
    is opened. It defaults to 'r' which means open for reading in text
    mode.  Other common values are 'w' for writing (truncating the file if
    it already exists), 'x' for creating and writing to a new file, and
    'a' for appending (which on some Unix systems, means that all writes
    append to the end of the file regardless of the current seek position).
    In text mode, if encoding is not specified the encoding used is platform
    dependent: locale.getpreferredencoding(False) is called to get the
    current locale encoding. (For reading and writing raw bytes use binary
    mode and leave encoding unspecified.) The available modes are:
```
其中，`file`为文档路径，`mode`为打开文件的模式。

关于`mode`，文档中有详细的说明：
```
========= ===============================================================
Character Meaning
--------- ---------------------------------------------------------------
'r'       open for reading (default)
'w'       open for writing, truncating the file first
'x'       create a new file and open it for writing
'a'       open for writing, appending to the end of the file if it exists
'b'       binary mode
't'       text mode (default)
'+'       open a disk file for updating (reading and writing)
'U'       universal newline mode (deprecated)
========= ===============================================================
```
### 文件对象方法
- close()

```
def close(self, )
close() -> None or (perhaps) an integer. Close the file.

Sets data attribute .closed to True. A closed file cannot be used for further I/O operations. close() may be called more than once without error. Some kinds of file objects (for example, opened by popen()) may return an exit status upon closing.
```
- read()

```
def read(self, size)
read([size]) -> read at most size bytes, returned as a string.

If the size argument is negative or omitted, read until EOF is reached. Notice that when in non-blocking mode, less data than what was requested may be returned, even if no size parameter was given.
```
- readline()

```
def readline(self, size)
readline([size]) -> next line from the file, as a string.

Retain newline. A non-negative size argument limits the maximum number of bytes to return (an incomplete line may be returned then). Return an empty string at EOF.
```
- write()

```
def write(self, str)
write(str) -> None. Write string str to file.

Note that due to buffering, flush() or close() may be needed before the file on disk reflects the data written.
```
- writelines()

```
def writelines(self, sequence_of_strings)
writelines(sequence_of_strings) -> None. Write the strings to the file.

Note that newlines are not added. The sequence can be any iterable object producing strings. This is equivalent to calling write() for each string.
```
- seek()

```
def seek(self, offset, whence)
seek(offset[, whence]) -> None. Move to new file position.

Argument offset is a byte count. Optional argument whence defaults to

0 (offset from start of file, offset should be  = 0); other values are 1  
(move relative to current position, positive or negative), and 2 (move relative to end of file, usually negative, although many platforms allow seeking beyond the end of a file). If the file is opened in text mode, only offsets returned by tell() are legal. Use of other offsets causes undefined behavior. Note that not all file objects are seekable.
```
- tell()

```
def tell(self, )
tell() -> current file position, an integer (may be a long integer).
```

## OS模块

模块是一个包含所有你定义的函数和变量的文件，其后缀名为.py。模块可以被别的程序引入，以使用该模块中的函数等功能。

### OS模块中关于文件、目录常用的函数使用方法
- getcwd()

```
def getcwd()
getcwd() -> path

Return a string representing the current working directory.
```
- chdir()

```
def chdir(path)
Change the current working directory to the specified path.
```
- listdir()

```
listdir(path) -> list_of_strings

Return a list containing the names of the entries in the directory.

    path: path of directory to list  
The list is in arbitrary order. It does not include the special entries '.' and '..' even if they are present in the directory.
```
- mkdir(), makedirs()

```
def mkdir(path, mode)
Create a directory.
```

```
def makedirs(name, mode=0777)
Super-mkdir; create a leaf directory and all intermediate ones. Works like mkdir, except that any intermediate path segment (not just the rightmost) will be created if it does not exist. This is recursive.
```
- remove()

```
def remove(path)
Remove a file (same as unlink(path)).
```
- rmdir(), removedirs()

```
def rmdir(path)
Remove a directory.
```

```
def removedirs(name)
Super-rmdir; remove a leaf directory and all empty intermediate ones. Works like rmdir except that, if the leaf directory is successfully removed, directories corresponding to rightmost path segments will be pruned away until either the whole path is consumed or an error occurs. Errors during this latter phase are ignored -- they generally mean that a directory was not empty.
```
- rename()

```
def rename(old, new)
Rename a file or directory.
```
- system()

```
def system(command)
system(command) -> exit_status

Execute the command (a string) in a subshell.
```
### 支持路径操作中常用的一些定义，支持所有平台

- os.curdir

表示当前目录，相当于`'.'`

- os.pardir

表示上一级目录，相当于`'..'`

- os.sep

输出系统特定的路径分隔符，相当于Windows中的`'\\'`，Linux中的`'/'`

- os.linesep

输出系统中使用的行终止符，相当于Windows中的`'\r\n'`，Linux中的`'\n'`

- os.name

表示当前使用的操作系统

## os.path模块

### 