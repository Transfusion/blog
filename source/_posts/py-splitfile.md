title: Python snippet that splits a target file into chunks.
url: 1.html
id: 1
categories:
  - Programming
date: 2012-01-20 14:47:13
tags:
---
```py
$ python testsplit.py -h
usage: testsplit.py [-h] -f FILESPLIT -c CHUNKS

File Splitting by Transfusion

optional arguments:
-h, --help show this help message and exit
-f FILESPLIT, --filesplit FILESPLIT
File, in current directory or entire path
-c CHUNKS, --chunks CHUNKS
Size of each Chunk in MB

```

py2 code:

```py
import os
import sys
import argparse
parser = argparse.ArgumentParser(description='File Splitting by Transfusion')
parser.add_argument('-f','--filesplit', help='File, in current directory or entire path', required=True)
parser.add_argument('-c','--chunks', type=int, help='Size of each Chunk in MB', required=True)
args = vars(parser.parse_args())
def splitFile(inputFile, chunkSizeMB):

    chunkSize = int(chunkSizeMB)*1048576
    #read the contents of the file
    f = open(inputFile, 'rb')
    data = f.read() # read the entire content of the file
    f.close()

    # get the length of data, ie size of the input file in bytes
    bytes = len(data)
    print bytes

    #calculate the number of chunks to be created
    noOfChunks = bytes/chunkSize
    if(bytes%chunkSize):
    noOfChunks+=1

    #create a info.txt file for writing metadata
    f = open(os.path.splitext(inputFile)[0]+'-info.txt', 'w')
    f.write(inputFile+','+'chunk,'+str(noOfChunks)+','+str(chunkSize))
    f.close()

    chunkNames = []
    for i in range(0, bytes+1, chunkSize):
    fn1 = os.path.splitext(inputFile)[0]+"ChunkByte%s" % i
    chunkNames.append(fn1)
    f = open(fn1, 'wb')
    f.write(data[i:i + chunkSize])
    f.close()

#try:
# with open(sys.argv[1]): pass
#except IOError:
# print 'Not a valid file.'

#if isinstance(int(sys.argv[2]),(int, long)) == False:
# print 'Please enter the filesize in MB, without using the letters MB'
splitFile(args['filesplit'], args['chunks'])
```

use 2to3 to convert to py3 code demo:

```bash
$ ls -lah
total 21M
drwxrwxr-x  2 transfusion transfusion 4.0K Sep 24 20:03 .
drwxr-xr-x 31 transfusion transfusion 4.0K Sep 24 19:13 ..
-rw-rw-r--  1 transfusion transfusion  10M Dec  5  2005 10mb.test
-rwxrwxr-x  1 transfusion transfusion 1.5K Sep 24 19:38 filesplit.py
```

```bash
$ python filesplit.py -f 10mb.test -c 4
10485760
```

```bash
$ ls -la
total 20504
drwxrwxr-x  2 transfusion transfusion     4096 Sep 24 20:03 .
drwxr-xr-x 31 transfusion transfusion     4096 Sep 24 19:13 ..
-rw-rw-r--  1 transfusion transfusion  4194304 Sep 24 20:03 10mbChunkByte0
-rw-rw-r--  1 transfusion transfusion  4194304 Sep 24 20:03 10mbChunkByte4194304
-rw-rw-r--  1 transfusion transfusion  2097152 Sep 24 20:03 10mbChunkByte8388608
-rw-rw-r--  1 transfusion transfusion       25 Sep 24 20:03 10mb-info.txt
-rw-rw-r--  1 transfusion transfusion 10485760 Dec  5  2005 10mb.test
-rwxrwxr-x  1 transfusion transfusion     1488 Sep 24 19:38 filesplit.py
```

```bash
$ cat 10mb-info.txt
10mb.test,chunk,3,4194304
```