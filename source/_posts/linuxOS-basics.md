---
title: linuxOS-basics
date: 2024-03-08 20:17:10
tags: linux
categories:
- linux config
---

## Copy-paste, move and remove file or folder

```bash
cp source_file(folder)  destination_folder  [-r]
```

```bash
mv source_file(folder) destination_folder

mv demo.txt test.txt //rename the file
```

```bash
rm file(folder)_name [-r -f -v -i]
```



## How to compress or decompress in linux

### basic infos

```reStructuredText
.tar VS .tar.gz VS .tgz >> 
".tar": This is the most basic archive file format, which bundles multiple files or directories into a single file without compression. Therefore, .tar files are commonly referred to as tarballs or tar archives.

".tar.gz": This is a file format compressed using the gzip compression algorithm on top of the .tar format. It bundles multiple files or directories into a .tar file, which is then compressed using gzip to create a .tar.gz file.

Hence, .tar.gz and .tgz are the same format, with different file extensions, both representing a file that has been bundled with tar and compressed with gzip.
```

### compress

#### Using tar and gzip:

```
tar -czvf ./archive.tar.gz /path/to/directory_or_file
```

- `-c`: Create a compressed file.
- `-z`: Use gzip compression.
- `-v`: Display detailed output.
- `-f`: Specify the name of the compressed file.
- `archive.tar.gz`: The name of the compressed file.
- `/path/to/directory_or_file`: The directory or file to be compressed.

#### Using zip:

```
zip -r ./archive.zip /path/to/directory_or_file
```

- `-r`: Recursively compress directories and their contents.
- `archive.zip`: The name of the compressed file.
- `/path/to/directory_or_file`: The directory or file to be compressed.



### decompress

#### Using tar and gzip:

```
tar -xzvf ./archive.tar.gz -C /output
```

- `-x`: Extract files.
- `-z`: Use gzip decompression.
- `-v`: Display detailed output.
- `-f`: Specify the file to be decompressed.
- `archive.tar.gz`: The name of the file to be decompressed.

#### Using unzip:

```
unzip ./archive.zip -d /output
```

- `archive.zip`: The name of the file to be decompressed.
