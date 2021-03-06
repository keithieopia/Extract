# `extract` in your console... *the next generation*

What’s a good way to extract: *.zip, .rar, .bz2, .gz, .tar, .tbz2, .tgz, .Z, .7z, .xz, .exe, .tar.bz2, .tar.gz, .tar.xz, .arj, .cab, .chm, .deb, .dmg, .iso, .lzh, .msi, .rpm, .udf, .wim, .xar .cpio* files on Mac or Linux?

The goal is to make `extract` able to extract anything you give it. The command `extract` uses the free unpackers to support many older and obscure formats.

## What's different about this version of `extract` compared to others?

### 1. Faster decompression
If they're installed, `extract` will detect and automatically use parallel / multithreaded compression tools such as: 

    * `pigz`
    * `pbzip2` or `lbzip2`
    * `pxz`
    * `plzip`

This usually reduces the time required to decompress large archives by half, if not more!

### 2. Better archive detection
Other versions use the archive's extension to figure out how to open it. That usually works until you come across:
    * a `.ZIP` that's really a `.RAR` or `.7z`
    * archives changed to look like images so they can be uploaded to imageboards
    * archives split into multiple volumes, e.g.: archive.r00, archive.r01, *etc*
    * downloading from a filehost that changes the name to random gibberish
    * you accidentally rename the file and forget to keep its extension

This version actually looks at the file's [content](https://en.wikipedia.org/wiki/List_of_file_signatures) to figure out what it is, regardless of it's extension.

### 3. Wider archive support
	* `.a`: deprecated Unix [archive file](https://en.wikipedia.org/wiki/Ar_%28Unix%29)
	* `.gif`: extract all the frames from an animated GIF, via ImageMagick (convert)
	* `.jar`: [Java Archives](https://docs.oracle.com/javase/tutorial/deployment/jar/)
	* `.lz4`: [LZ4 compression](https://github.com/lz4/lz4)
    * `.lzo`: Lempel–Ziv–Oberhumer compression, via [lzop](https://www.lzop.org/)
    * `.rpa`: Ren'Py game archives, via [unrpa](https://github.com/Lattyware/unrpa) or [rpatool](https://github.com/Shizmob/rpatool)

### 4. Better fallbacks
7-Zip opens practically everything, but `extract` should try to use other programs
if the user doesn't have it installed. 

Other versions tend to rely heavily on 7-Zip. While it does opens practically 
everything, `extract` should try to use other programs if the user doesn't have 
7-zip installed. 

### 4. Better cross-platform support

#### 7-Zip differences
Package names for 7-Zip vary greatly between operating systems and Linux distributions (e.g.: `7z`, `7za`, and `7zr`), this version of `extract` find which is installed, and if all are available, it intelligently picks the most feature rich version.

#### Shell Agnostic
By converting `extract` to a shell script, users can use `extract` with their favorite shell. Previously, `extract` was a BASH function which was not compatible with other shells such as Zsh and Fish.

Furthermore, a single file shell script is:

    * Easier to update (and arguably install)
    * Easier to debug, test, and contribute
    * Easier to install globally for all users


## How to install

### Ubuntu, Debian, Fedora, CentOS, and all derivatives:

```console
$ mkdir -p ~/.local/bin
$ cp extract ~/.local/bin
```

### macOS / Mac OS X

Copy and paste `extract` into `/usr/local/bin`:

```console
$ sudo mkdir -p /usr/local/bin
$ sudo cp extract /usr/local/bin
```

### Global install for Linux
Follow the **macOS / Mac OS X** instructions if you want to make extract available for all user account on Linux


### Lightweight Linux Distros

You may need to add `~/.local/bin` to your $PATH:

```console
$ mkdir -p ~/.local/bin
$ cp extract ~/.local/bin
$ echo 'export PATH=~/.local/bin:$PATH' >> ~/.bashrc
```

#### *HEY! I don't use BASH!*:

Follow the first two steps above, then change the `echo` line accordingly:

**Zsh:**
```console
$ echo 'export PATH=~/.local/bin:$PATH' >> ~/.zshrc
```

**Fish:**
```console
$ echo 'set PATH ~/.local/bin $PATH'
```

#### *HEY! Binaries go in ~/bin*
I agree, if it's already in your $PATH, just drop `extract` into `~/bin`

## How it use

Using command `extract`, in a terminal

```
$ extract <archive_filename.extention>

$ extract <archive_filename_1.extention> <archive_filename_2.extention> <archive_filename_3.extention> ...
```

## License
Copyright &copy; [Timothy Keith](http://keithieopia.com) and [Vitalii Tereshchuk](http://dotoca.net), licensed under the MIT license.
