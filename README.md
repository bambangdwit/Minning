CPUMiner-Multi
Build Status

This is a multi-threaded CPU miner, fork of pooler's cpuminer (see AUTHORS for list of contributors).

Table of contents
Algorithms
Dependencies
Download
Build
Usage instructions
Donations
Credits
License
Algorithms
Currently supported
✓ scrypt (Litecoin, Dogecoin, Feathercoin, ...)
✓ scrypt:N
✓ scrypt-jane:N
✓ sha256d (Bitcoin, Freicoin, Peercoin/PPCoin, Terracoin, ...)
✓ allium (Garlicoin, Tuxcoin)
✓ axiom (Axiom Shabal-256 based MemoHash)
✓ bastion (Joincoin [J])
✓ bitcore Permuted serie of 10 algos (BitCore)
✓ blake (Saffron [SFR] Blake-256)
✓ blake2s (NevaCoin Blake2-S 256)
✓ blake2b (Not SIA one)
✓ bmw (Midnight [MDT] BMW-256)
✓ cryptonight (Bytecoin [BCN], Monero [XMR])
✓ cryptonight-light (Aeon)
✓ decred (Blake256-14 [DCR])
✓ dmd-gr (Diamond-Groestl)
✓ fresh (FreshCoin)
✓ geek (GeekCash [GEEK])
✓ groestl (Groestlcoin)
✓ jha (JackpotCoin, SweepStake)
✓ lbry (LBRY Credits [LBC])
✓ lyra2RE (Cryptocoin)
✓ lyra2REv2
✓ lyra2REv3 (VertCoin [VTC])
✓ myr-gr Myriad-Groestl (MyriadCoin [MYR])
✓ neoscrypt (Feathercoin)
✓ nist5 (MistCoin [MIC], TalkCoin [TAC], ...)
✓ pentablake (Joincoin)
✓ pluck (Supcoin [SUP])
✓ quark (Quarkcoin)
✓ qubit (GeoCoin)
✓ skein (Skeincoin, Myriadcoin, Xedoscoin, ...)
✓ skein2 (Woodcoin)
✓ s3 (OneCoin)
✓ sia (Reversed Blake2B for SIA [SC])
✓ sib X11 + gost streebog (SibCoin)
✓ timetravel Permuted serie of 8 algos (MachineCoin [MAC])
✓ tribus 3 of the top NIST5 algos (Denarius [DNR])
✓ vanilla (Blake-256 8-rounds - double sha256 [VNL])
✓ veltor (Veltor [VLT])
✓ xevan x17 x 2 on bigger header (BitSend [BSD])
✓ x11evo (Revolver [XRE])
✓ x11 (Darkcoin [DRK], Hirocoin, Limecoin, ...)
✓ x12 (GalaxyCash [GCH])
✓ x13 (Sherlockcoin, [ACE], [B2B], [GRC], [XHC], ...)
✓ x14 (X14, Webcoin [WEB])
✓ x15 (RadianceCoin [RCE])
✓ x16r (Ravencoin [RVN])
✓ x16s (Pigeoncoin [PGN])
✓ x17 (Verge [XVG])
✓ x20r
✓ yescrypt (GlobalBoostY [BSTY], Unitus [UIS], MyriadCoin [MYR])
✓ zr5 (Ziftrcoin [ZRC])
Implemented, but untested
? hefty1 (Heavycoin)
? keccak (Maxcoin HelixCoin, CryptoMeth, Galleon, 365coin, Slothcoin, BitcointalkCoin)
? keccakc (Creativecoin)
? luffa (Joincoin, Doomcoin)
? rainforest
? shavite3 (INKcoin)
Planned support for
scrypt-jane (YaCoin, CopperBars, Pennies, Tickets, etc..)
Dependencies
libcurl http://curl.haxx.se/libcurl/
jansson http://www.digip.org/jansson/ (jansson source is included in-tree)
openssl libcrypto https://www.openssl.org/
pthreads
zlib (for curl/ssl)
Download
Windows releases: https://github.com/tpruvot/cpuminer-multi/releases
Git tree: https://github.com/tpruvot/cpuminer-multi
Clone with git clone https://github.com/tpruvot/cpuminer-multi
Build
Basic *nix build instructions:
just use ./build.sh OR
 ./autogen.sh	# only needed if building from git repo
 ./nomacro.pl	# only needed if building on Mac OS X or with Clang
 ./configure CFLAGS="*-march=native*" --with-crypto --with-curl
 # Use -march=native if building for a single machine
 make
Note for Debian/Ubuntu users:
 apt-get install automake autoconf pkg-config libcurl4-openssl-dev libjansson-dev libssl-dev libgmp-dev make g++
Note for OS X users:
 brew install openssl curl
 ./build.sh # if curl was installed to /usr/local/opt, else update build.sh paths in darwin section
Note for pi64 users:
 ./autogen.sh
 ./configure --disable-assembly CFLAGS="-Ofast -march=native" --with-crypto --with-curl
Notes for AIX users:
To build a 64-bit binary, export OBJECT_MODE=64
GNU-style long options are not supported, but are accessible via configuration file
Basic Windows build with Visual Studio 2013
All the required .lib files are now included in tree (windows only)
AVX enabled by default for x64 platform (AVX2 and XOP could also be used)
Basic Windows build instructions, using MinGW64:
Install MinGW64 and the MSYS Developer Tool Kit (http://www.mingw.org/)
Make sure you have mstcpip.h in MinGW\include
install pthreads-w64
Install libcurl devel (http://curl.haxx.se/download.html)
Make sure you have libcurl.m4 in MinGW\share\aclocal
Make sure you have curl-config in MinGW\bin
Install openssl devel (https://www.openssl.org/related/binaries.html)
In the MSYS shell, run:
for 64bit, you can use ./mingw64.sh else : ./autogen.sh	# only needed if building from git repo
LIBCURL="-lcurldll" ./configure CFLAGS="*-march=native*"
# Use -march=native if building for a single machine
make
Architecture-specific notes:
ARM:
No runtime CPU detection. The miner can take advantage of some instructions specific to ARMv5E and later processors, but the decision whether to use them is made at compile time, based on compiler-defined macros.
To use NEON instructions, add "-mfpu=neon" to CFLAGS.
x86:
The miner checks for SSE2 instructions support at runtime, and uses them if they are available.
x86-64:
The miner can take advantage of AVX, AVX2 and XOP instructions, but only if both the CPU and the operating system support them.
Linux supports AVX starting from kernel version 2.6.30.
FreeBSD supports AVX starting with 9.1-RELEASE.
Mac OS X added AVX support in the 10.6.8 update.
Windows supports AVX starting from Windows 7 SP1 and Windows Server 2008 R2 SP1.
The configure script outputs a warning if the assembler doesn't support some instruction sets. In that case, the miner can still be built, but unavailable optimizations are left off.
Usage instructions
Run "cpuminer --help" to see options.

Connecting through a proxy
Use the --proxy option.

To use a SOCKS proxy, add a socks4:// or socks5:// prefix to the proxy host
Protocols socks4a and socks5h, allowing remote name resolving, are also available since libcurl 7.18.0.

If no protocol is specified, the proxy is assumed to be a HTTP proxy.
When the --proxy option is not used, the program honors the http_proxy and all_proxy environment variables.

Donations
Donations for the work done in this fork are accepted :

Tanguy Pruvot :

BTC: 1FhDPLPpw18X4srecguG3MxJYe4a1JsZnd
Lucas Jones :

MRO: 472haywQKoxFzf7asaQ4XKBc2foAY4ezk8HiN63ifW4iAbJiLnfmJfhHSR9XmVKw2WYPnszJV9MEHj9Z5WMK9VCNHaGLDmJ
BTC: 139QWoktddChHsZMWZFxmBva4FM96X2dhE
Credits
CPUMiner-multi was forked from pooler's CPUMiner, and has been started by Lucas Jones.

tpruvot added all the recent features and newer algorythmns
Wolf9466 helped with Intel AES-NI support for CryptoNight
License
GPLv2. See COPYING for details.
