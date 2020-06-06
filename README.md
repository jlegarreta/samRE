# samRE
samRE is a toolkit for reverse engineering Samsung Android ROMs, featuring a script I wrote called [samdump](../master/bin/samdump).

Given a Samsung firmware ROM, the samdump script will:
* Untar the ROM file
* Decompress the images
* Convert the images to raw format
* Mount the images
* Extract the filesystems
* Unpack the APKs
* Convert the VDEX files to DEX (in some cases, extract the CDEX from the VDEX and convert to DEX)
* Convert the DEX files to JAR
* Decompile all the JARs to Java source code.

Currently, this tool is designed to run on Mac OS X, however with some minor modifications should be able to run on Linux. This is on my to-do list.
## Dependencies
The samdump script depends on [lz4](https://github.com/lz4/lz4) and [ext4fuse](https://github.com/gerard/ext4fuse) (which requires [osxfuse](https://osxfuse.github.io/)). It also depends on GNU [parallel](https://www.gnu.org/software/parallel/) as samdump takes advantage of parallel processing to reduce the amount of time it takes to decompile files. You can install all these dependencies via homebrew:
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
* [dex2jar](https://github.com/pxb1988/dex2jar) (commit [d7a86110](https://github.com/pxb1988/dex2jar/tree/d7a86110baba3f845973017021fb10664b1b90d2))
* [vdexExtractor](https://github.com/anestisb/vdexExtractor) (commit [3fa69ec](https://github.com/anestisb/vdexExtractor/tree/78f283b60ab6991fa27eeaff7d7be16409401c08))
* [compact_dex_converter](https://github.com/anestisb/vdexExtractor/blob/master/README.md) (commit [3fa69ec](https://github.com/anestisb/vdexExtractor/tree/78f283b60ab6991fa27eeaff7d7be16409401c08))
* [apktool](https://ibotpeaches.github.io/Apktool) (version 2.4.1)
* [cfr](https://www.benf.org/other/cfr) (version 0.150)
* [simg2img](https://android.googlesource.com/platform/system/core/+/refs/heads/master/libsparse) (commit [c44f50c](https://android.googlesource.com/platform/system/core/+/c44f50ca587aefac5505a1f1298e5c01da63baca))
* [Heimdall](https://gitlab.com/BenjaminDobell/Heimdall) (version 1.4.2)
