# samRE
samRE is a toolkit for reverse engineering Samsung Android ROMs, featuring a script I wrote called [samdump](../master/bin/samdump).

Given a Samsung firmware ROM, the samdump script will:
* Untar the ROM file
* Decompress the images
* Convert the images to raw format
* Mount the images
* Extract the filesystems
* Unpack the APKs
* Convert the VDEX files to DEX
* Convert the DEX files to JAR
* Decompile all the JARs to Java source code.

Currently, this tool is designed to run on Mac OS X, however with some minor modifications should be able to run on Linux. This is on my to-do list.
## Dependencies
The samdump script depends on [lz4](https://github.com/lz4/lz4) and [ext4fuse](https://osxfuse.github.io/) (which requires osxfuse). It also depends on GNU [parallel](https://www.gnu.org/software/parallel/) as samdump takes advantage of parallel processing to reduce the amount of time it takes to decompile files. You can install these dependencies in homebrew:
```
brew cask install osxfuse
brew install lz4 ext4fuse parallel
```
You will also need [Java](https://www.oracle.com/java/). This has been tested with JDK 14.0.1 on MacOS 10.15.4.

NOTE: I highly suggest using a case-sensitive partition/APFS container or disk image for running these tools to avoid conflicts.
## Usage
```
source activate
samdump SAMSUMG_ROM.tar.md5
```
## Included tools
* [dex2jar](https://github.com/pxb1988/dex2jar)
* [vdexExtractor](https://github.com/anestisb/vdexExtractor)
* [compact_dex_converter](https://github.com/anestisb/vdexExtractor)
* [apktool](https://ibotpeaches.github.io/Apktool)
* [cfr](https://www.benf.org/other/cfr)
* [simg2img](https://android.googlesource.com/platform/system/core/+/refs/heads/master/libsparse)
