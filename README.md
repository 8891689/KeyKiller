# KeyKiller
KeyKiller is the world's highest-performing CPU-based Satoshi puzzle solver, leveraging modern CPU instruction sets like AVX2 and AVX512 to achieve unparalleled computational performance. Deeply optimized for Linux and Windows operating systems, it strikes a balance between speed and accuracy, making it the ultimate tool for cryptographic puzzle solving.

Our Secp256k1 implementation draws upon the excellent projects of Jean-Luc Pons/VanitySearch (https://github.com/JeanLucPons/VanitySearch) and albertobsd/keyhunt (https://github.com/albertobsd/keyhunt), which have been adapted and improved. We are deeply grateful to Jean-Luc Pons and albertobsd for their foundational contributions to the cryptographic community.




1. Deep optimization has been performed, including reimplementation of the underlying computational library and some extremely difficult instruction-level adjustments. All computations will be performed in the kernel.

2. Deep rationalization has been done in some modes, and logical comparisons and calculations have been reimplemented.

3. Although the bottom and top layers have been reimplemented, all logical commands are retained and there are not many changes from the original version.

4. I'm sorry, please forgive me. Developing more programs requires time and financial support. This program is only available to members who have purchased a compressed password. The source code will be released in 5 years.

5. Next, we will use data for comparison to see the effects of optimization.


```
./keyhunt -h
[+] Version 1.0 Technical Support: github.com/8891689

Usage:
-h          show this help
-B Mode     BSGS now have some modes <sequential, backward, both, random, dance>
-b bits     For some puzzles you only need some numbers of bits in the test keys.
-c crypto   Search for specific crypto. <btc, eth> valid only w/ -m address
-C mini     Set the minikey Base only 22 character minikeys, ex: SRPqx8QiwnW4WNWnTVa2W5
-8 alpha    Set the bas58 alphabet for minikeys
-e          Enable endomorphism search (Only for address, rmd160 and vanity)
-f file     Specify file name with addresses or xpoints or uncompressed public keys
-I stride   Stride for xpoint, rmd160 and address, this option don't work with bsgs
-k value    Use this only with bsgs mode, k value is factor for M, more speed but more RAM use wisely
-l look     What type of address/hash160 are you looking for <compress, uncompress, both> Only for rmd160 and address
-m mode     mode of search for cryptos. (bsgs, xpoint, rmd160, address, vanity) default: address
-M          Matrix screen, feel like a h4x0r, but performance will dropped
-n number   Check for N sequential numbers before the random chosen, this only works with -R option
            Use -n to set the N for the BSGS process. Bigger N more RAM needed
-q          Quiet the thread output
-r SR:EN    StarRange:EndRange, the end range can be omitted for search from start range to N-1 ECC value
-R          Random, this is the default behavior
-s ns       Number of seconds for the stats output, 0 to omit output.
-S          S is for SAVING in files BSGS data (Bloom filters and bPtable)
-6          to skip sha256 Checksum on data files-t tn       Threads number, must be a positive integer
-v value    Search for vanity Address, only with -m vanity
-z value    Bloom size multiplier, only address,rmd160,vanity, xpoint, value >= 1

Example:

./keyhunt -m rmd160 -f 71_Puzzle_hash160.txt -b 71 -l compress -R -t 4

```


## address mode

```
./keyhunt -m address -f tests/66.txt -b 66 -l compress -R
[+] Version 0.2.230519 Satoshi Quest, developed by AlbertoBSD
[+] Mode address
[+] Search compress only
[+] Random mode
[+] Setting search for btc adddress
[+] N = 0x100000000
[+] Bit Range 66
[+] -- from : 0x20000000000000000
[+] -- to   : 0x40000000000000000
[+] Allocating memory for 1 elements: 0.00 MB
[+] Bloom filter for 1 elements.
[+] Loading data to the bloomfilter total: 0.03 MB
[+] Sorting data ... done! 1 values were loaded and sorted
^C] Total 92090368 keys in 30 seconds: ~3 Mkeys/s (3069678 keys/s)


./keyhunt -m address -f tests/66.txt -b 66 -l compress -R
[+] Version 1.0 Technical Support: github.com/8891689
[+] Mode address
[+] Search compress only
[+] Random mode
[+] Setting search for btc adddress
[+] N = 0x100000000
[+] Bit Range 66
[+] -- from : 0x20000000000000000
[+] -- to   : 0x40000000000000000
[+] Allocating memory for 1 elements: 0.00 MB
[+] Bloom filter for 1 elements.
[+] Loading data to the bloomfilter total: 0.03 MB
[+] Sorting data ... done! 1 values were loaded and sorted
^C] Total 124551168 keys in 30 seconds:  ~4 Mkeys/s (4151705 keys/s)
```

### vanity search.

```
./keyhunt -m vanity -l compress -R -b 256 -v 1Good1 -v 1MyKey
[+] Version 0.2.230519 Satoshi Quest, developed by AlbertoBSD
[+] Mode vanity
[+] Search compress only
[+] Random mode
[+] Added Vanity search : 1Good1
[+] Added Vanity search : 1MyKey
[+] N = 0x100000000
[+] Bit Range 256
[+] -- from : 0x8000000000000000000000000000000000000000000000000000000000000000
[+] -- to   : 0xfffffffffffffffffffffffffffffffebaaedce6af48a03bbfd25e8cd0364141
[+] Bloom filter for 4 elements.
[+] Loading data to the bloomfilter total: 0.03 MB
Base key: b2d85a96c96ab4bb1c8fc572307f7330540e75aea89dfefa79fac467d2df934f 
Vanity Private Key: 4d27a56936954b44e3703a8dcf808cce66a0673806aaa14145d79a24fb29594f
pubkey: 03cbcfba28769c737d53509a03b3240405cc19e125d464adf65f1db5d44b022381
Address 1Good1W5K1GNPCFoR9USjy4SSawQKfCRQx
rmd160 ad63f02851ff8834e17041ab331ae8c51dded979
^C] Total 91410432 keys in 30 seconds: ~3 Mkeys/s (3047014 keys/s)



./keyhunt -m vanity -l compress -R -b 256 -v 1Good1 -v 1MyKey
[+] Version 1.0 Technical Support: github.com/8891689
[+] Mode vanity
[+] Search compress only
[+] Random mode
[+] Added Vanity search : 1Good1
[+] Added Vanity search : 1MyKey
[+] N = 0x100000000
[+] Bit Range 256
[+] -- from : 0x8000000000000000000000000000000000000000000000000000000000000000
[+] -- to   : 0xfffffffffffffffffffffffffffffffebaaedce6af48a03bbfd25e8cd0364141
[+] Bloom filter for 4 elements.
[+] Loading data to the bloomfilter total: 0.03 MB
[+] Total 123152384 keys in 30 seconds:  ~4 Mkeys/s (4105079 keys/s)
[!]Key: e3331f946f4e2ebf27aa9eb11845137602b561956cff67b75f711d26e7a9f251
[!]pub: 03bda9547f16dc27739efd04e96c1086e02cddfb7aa656f077ecbf7dd56f5a9806
[!]Add: 1MyKeykKESGddsADhBZ786MLc3crNhkRiQ
[!]rmd: e60961bc3c02e06ea1420bfd731d83f0362f1634

[!]Key: 1ccce06b90b1d140d855614ee7baec88b7f97b514249388460614165e735d575
[!]pub: 027e0af878fa75bb610f12c0348d59cdbf112f7ff5dad922bda4ffe8763375cb2e
[!]Add: 1Good1wmaF9QwtcFTrNVyQaMF9dB15N1CK
[!]rmd: ad63f02f864c152d26374f6636d1c714705d9c58

[!]Key: e3331f946f4e2ebf27aa9eb11845137602b561956cff67b75f711d26e9ec80ae
[!]pub: 027d76203462f21515915aec87100bbfcc27f5e02f4b92cacaf39d99c258b19f1e
[!]Add: 1MyKey7tioVEfc6ETkZjr9LAJ973BkHGih
[!]rmd: e60961b205a387fc4868f6805a7176b495477c59
^C] Total 246380544 keys in 60 seconds:  ~4 Mkeys/s (4106342 keys/s)
```

## rmd160 mode
```
./keyhunt -m rmd160 -f tests/1to32.rmd -r 11111111:FFFFFFFFFF -l compress -s 5
[+] Version 0.2.230519 Satoshi Quest, developed by AlbertoBSD
[+] Mode rmd160
[+] Search compress only
[+] Stats output every 5 seconds
[+] N = 0x100000000
[+] Range 
[+] -- from : 0x11111111
[+] -- to   : 0xffffffffff
[+] Allocating memory for 32 elements: 0.00 MB
[+] Bloom filter for 32 elements.
[+] Loading data to the bloomfilter total: 0.03 MB
[+] Sorting data ... done! 32 values were loaded and sorted
^C] Total 30703616 keys in 10 seconds: ~3 Mkeys/s (3070361 keys/s)

Endomorphism -e

./keyhunt -m rmd160 -f tests/1to32.rmd -r 11111111:FFFFFFFFFF -l compress -s 5 -e
[+] Version 0.2.230519 Satoshi Quest, developed by AlbertoBSD
[+] Mode rmd160
[+] Search compress only
[+] Stats output every 5 seconds
[+] Endomorphism enabled
[+] N = 0x100000000
[+] Range 
[+] -- from : 0x11111111
[+] -- to   : 0xffffffffff
[+] Allocating memory for 32 elements: 0.00 MB
[+] Bloom filter for 32 elements.
[+] Loading data to the bloomfilter total: 0.03 MB
[+] Sorting data ... done! 32 values were loaded and sorted
^C] Total 18223104 keys in 5 seconds: ~3 Mkeys/s (3644620 keys/s)



./keyhunt -m rmd160 -f tests/1to32.rmd -r 11111111:FFFFFFFFFF -l compress -s 5
[+] Version 1.0 Technical Support: github.com/8891689
[+] Mode rmd160
[+] Search compress only
[+] Stats output every 5 seconds
[+] N = 0x100000000
[+] Range 
[+] -- from : 0x11111111
[+] -- to   : 0xffffffffff
[+] Allocating memory for 32 elements: 0.00 MB
[+] Bloom filter for 32 elements.
[+] Loading data to the bloomfilter total: 0.03 MB
[+] Sorting data ... done! 32 values were loaded and sorted
^C] Total 60602368 keys in 15 seconds:  ~4 Mkeys/s (4040157 keys/s)

Endomorphism -e

./keyhunt -m rmd160 -f tests/1to32.rmd -r 11111111:FFFFFFFFFF -l compress -s 5 -e
[+] Version 1.0 Technical Support: github.com/8891689
[+] Mode rmd160
[+] Search compress only
[+] Stats output every 5 seconds
[+] Endomorphism enabled
[+] N = 0x100000000
[+] Range 
[+] -- from : 0x11111111
[+] -- to   : 0xffffffffff
[+] Allocating memory for 32 elements: 0.00 MB
[+] Bloom filter for 32 elements.
[+] Loading data to the bloomfilter total: 0.03 MB
[+] Sorting data ... done! 32 values were loaded and sorted
^C] Total 51677184 keys in 10 seconds:  ~5 Mkeys/s (5167718 keys/s)

```

## xpoint mode
```

./keyhunt -m xpoint -f tests/substracted40.txt -n 65536 -t 4 -b 40
[+] Version 0.2.230519 Satoshi Quest, developed by AlbertoBSD
[+] Mode xpoint
[+] Threads : 4
[+] N = 0x10000
[+] Bit Range 40
[+] -- from : 0x8000000000
[+] -- to   : 0x10000000000
[+] Allocating memory for 6003 elements: 0.11 MB
[+] Bloom filter for 6003 elements.
[+] Loading data to the bloomfilter total: 0.03 MB
[+] Sorting data ... done! 6003 values were loaded and sorted
Base key: 8002590000 
Hit! Private Key: 800258a2ce
pubkey: 0474241b684e7c31e7933510b510aa14de9ac88ec3635bdd35a3bcf1d16da210be7ad946c9b185433fff3a7824ee140b15789d5f12d60cd2814154b0f8f1a4308e
Address 1CMg4mukBGVvid4ocTx5x5LEuCatKoHQRB
rmd160 7c92500fa9d2ecbca5bdd61bb6a14a249669bae4
Base key: 8009c20000 
Hit! Private Key: 8009c16fb9
pubkey: 047c3463c3d4e034f328749e2ac17b47a24b42ad47aaab0ec09d4d0abeee3ab46d097cc24d316210ad96b14db3c0f6ce045547f5af6a8d59589779d3f414720808
Address 1CrTyFmhGxrn3oREGwbaaHh7DZSK1cZvnt
rmd160 82044772bfc56eb51b47fa12ebbe59325b734b1e
Base key: 8011bd0000 
Hit! Private Key: 8011ba8af7
pubkey: 042b7ca30a99b5d3320f8a1501fca43d8de3cc6c0cc493b4be41081990f3b86d2ac29bea3941f2a8f93d8172792cd4530d44a2a76e2a17987ce490d6a61e58cbd5
Address 1Di7AnobY6cXBW2Yn3E27Nuv4nojHx54Lr
rmd160 8b67b699c3178171ebd46de8ea75b4ba2efd5d4d
Base key: 8014b00000 
Hit! Private Key: 8014af99e0
pubkey: 0483c8be25bfb8a43043f0ecbb2c77f47d61ce89e057b11d6a69b37efd56de1b7c3c358874d1374c4735f7ab79a676ea93697ba574873452f998889bca70a1fb07
Address 18c6Zb2zRAGRY2g8d5pCTQxL4npYPaf2cE
rmd160 536c14fa0c1d6ad7a53df6e8fd9b66473bf873db
Base key: 80172e0000 
Hit! Private Key: 80172ba39b
pubkey: 042feae0f91d650ec90bd3e0d69c9642cf7e203b872ff5ce7ed791683926fa1fd6d6516945da383c25a3dbb38358a961c4cdb6a9873d4447167c568069561a1c9e
Address 14mkcKHZgrzhQNnCHVXcnkUaWnzsU3iLLN
rmd160 295f1520e44fac7be31c8fcaf45d5fa4f20c85ad
^Cse key: 801cb40000     in 30 seconds: ~15 Mkeys/s (15034026 keys/s)




./keyhunt -m xpoint -f tests/substracted40.txt -n 65536 -t 4 -b 40
[+] Version 1.0 Technical Support: github.com/8891689
[+] Mode xpoint
[+] Threads : 4
[+] N = 0x10000
[+] Bit Range 40
[+] -- from : 0x8000000000
[+] -- to   : 0x10000000000
[+] Allocating memory for 6003 elements: 0.11 MB
[+] Bloom filter for 6003 elements.
[+] Loading data to the bloomfilter total: 0.03 MB
[+] Sorting data ... done! 6003 values were loaded and sorted
Base key: 80025b0000 
[!]Key: 800258a2ce
[!]pub: 0474241b684e7c31e7933510b510aa14de9ac88ec3635bdd35a3bcf1d16da210be7ad946c9b185433fff3a7824ee140b15789d5f12d60cd2814154b0f8f1a4308e
[!]Add: 1CMg4mukBGVvid4ocTx5x5LEuCatKoHQRB
[!]rmd: 7c92500fa9d2ecbca5bdd61bb6a14a249669bae4
Base key: 8009c30000 
[!]Key: 8009c16fb9
[!]pub: 047c3463c3d4e034f328749e2ac17b47a24b42ad47aaab0ec09d4d0abeee3ab46d097cc24d316210ad96b14db3c0f6ce045547f5af6a8d59589779d3f414720808
[!]Add: 1CrTyFmhGxrn3oREGwbaaHh7DZSK1cZvnt
[!]rmd: 82044772bfc56eb51b47fa12ebbe59325b734b1e
Base key: 8011bc0000 
[!]Key: 8011ba8af7
[!]pub: 042b7ca30a99b5d3320f8a1501fca43d8de3cc6c0cc493b4be41081990f3b86d2ac29bea3941f2a8f93d8172792cd4530d44a2a76e2a17987ce490d6a61e58cbd5
[!]Add: 1Di7AnobY6cXBW2Yn3E27Nuv4nojHx54Lr
[!]rmd: 8b67b699c3178171ebd46de8ea75b4ba2efd5d4d
Base key: 8014b10000 
[!]Key: 8014af99e0
[!]pub: 0483c8be25bfb8a43043f0ecbb2c77f47d61ce89e057b11d6a69b37efd56de1b7c3c358874d1374c4735f7ab79a676ea93697ba574873452f998889bca70a1fb07
[!]Add: 18c6Zb2zRAGRY2g8d5pCTQxL4npYPaf2cE
[!]rmd: 536c14fa0c1d6ad7a53df6e8fd9b66473bf873db
Base key: 80172d0000 
[!]Key: 80172ba39b
[!]pub: 042feae0f91d650ec90bd3e0d69c9642cf7e203b872ff5ce7ed791683926fa1fd6d6516945da383c25a3dbb38358a961c4cdb6a9873d4447167c568069561a1c9e
[!]Add: 14mkcKHZgrzhQNnCHVXcnkUaWnzsU3iLLN
[!]rmd: 295f1520e44fac7be31c8fcaf45d5fa4f20c85ad
^Cse key: 80241a0000     in 30 seconds:  ~19 Mkeys/s (19331481 keys/s)

```

## bsgs mode
```
./keyhunt -m bsgs -f tests/125.txt -R -b 125 -q -S -s 10
[+] Version 0.2.230519 Satoshi Quest, developed by AlbertoBSD
[+] Random mode
[+] Quiet thread output
[+] Stats output every 10 seconds
[+] Mode BSGS random
[+] Opening file tests/125.txt
[+] Added 1 points from file
[+] Bit Range 125
[+] -- from : 0x10000000000000000000000000000000
[+] -- to   : 0x20000000000000000000000000000000
[+] N = 0x100000000000
[+] Bloom filter for 4194304 elements : 14.38 MB
[+] Bloom filter for 131072 elements : 0.88 MB
[+] Bloom filter for 4096 elements : 0.88 MB
[+] Allocating 0.00 MB for 4096 bP Points
[+] processing 4194304/4194304 bP points : 100% 
[+] Making checkums .. ... done
[+] Sorting 4096 elements... Done!
[+] Writing bloom filter to file keyhunt_bsgs_4_4194304.blm .... Done!
[+] Writing bloom filter to file keyhunt_bsgs_6_131072.blm .... Done!
[+] Writing bP Table to file keyhunt_bsgs_2_4096.tbl .. Done!
[+] Writing bloom filter to file keyhunt_bsgs_7_4096.blm .... Done!
^C] Total 316659348799488 keys in 10 seconds: ~31 Tkeys/s (31665934879948 keys/s)



./keyhunt -m bsgs -f tests/125.txt -R -b 125 -q -S -s 10
[+] Version 1.0 Technical Support: github.com/8891689
[+] Random mode
[+] Quiet thread output
[+] Stats output every 10 seconds
[+] Mode BSGS random
[+] Opening file tests/125.txt
[+] Added 1 points from file
[+] Bit Range 125
[+] -- from : 0x10000000000000000000000000000000
[+] -- to   : 0x20000000000000000000000000000000
[+] N = 0x100000000000
[+] Bloom filter for 4194304 elements : 14.38 MB
[+] Bloom filter for 131072 elements : 0.88 MB
[+] Bloom filter for 4096 elements : 0.88 MB
[+] Allocating 0.00 MB for 4096 bP Points
[+] processing 4194304/4194304 bP points : 100% 
[+] Making checkums .. ... done
[+] Sorting 4096 elements... Done!
[+] Writing bloom filter to file keyhunt_bsgs_4_4194304.blm .... Done!
[+] Writing bloom filter to file keyhunt_bsgs_6_131072.blm .... Done!
[+] Writing bP Table to file keyhunt_bsgs_2_4096.tbl .. Done!
[+] Writing bloom filter to file keyhunt_bsgs_7_4096.blm .... Done!
^C] Total 316659348799488 keys in 10 seconds:  ~31 Tkeys/s (31665934879948 keys/s)
```
## minikeys mode

```
./keyhunt -m minikeys -f tests/minikeys.txt -C SG64GZqySYwBm9KxE1wJ28
[+] Version 0.2.230519 Satoshi Quest, developed by AlbertoBSD
[+] Mode minikeys
[+] N = 0x100000000
[+] Base Minikey : SG64GZqySYwBm9KxE1wJ28
[+] Allocating memory for 1 elements: 0.00 MB
[+] Bloom filter for 1 elements.
[+] Loading data to the bloomfilter total: 0.03 MB
[+] Sorting data ... done! 1 values were loaded and sorted
[+] Base minikey: SG64GZqySYwBm9KxE1wJ28? 
HIT!! Private Key: d1a4fc1f83b2f3b31dcd999acd8288ff346f7df46401596d53964e0c69d5b4d
pubkey: 048722093a2b5dd05a84c28a18b2a6601320c9eaab9db99e76b850f9574cd3d5c987bf0c9c9ed3bd0f52124a57d9ef292b529536b225b90f8760d9c67cc3aa1c32
minikey: SG64GZqySYwBm9KxE3wJ29
address: 15azScMmHvFPAQfQafrKr48E9MqRRXSnVv
^C] Total 567296 keys in 30 seconds: 18909 keys/s


./keyhunt -m minikeys -f tests/minikeys.txt -C SG64GZqySYwBm9KxE1wJ28
[+] Version 1.0 Technical Support: github.com/8891689
[+] Mode minikeys
[+] N = 0x100000000
[+] Base Minikey : SG64GZqySYwBm9KxE1wJ28
[+] Allocating memory for 4 elements: 0.00 MB
[+] Bloom filter for 4 elements.
[+] Loading data to the bloomfilter total: 0.03 MB
[+] Sorting data ... done! 4 values were loaded and sorted
[+] Base minikey: SG64GZqySYwBm9KxE1wJ28?
[!]Key: d1a4fc1f83b2f3b31dcd999acd8288ff346f7df46401596d53964e0c69d5b4d
[!]pub: 048722093a2b5dd05a84c28a18b2a6601320c9eaab9db99e76b850f9574cd3d5c987bf0c9c9ed3bd0f52124a57d9ef292b529536b225b90f8760d9c67cc3aa1c32
[!]wif: SG64GZqySYwBm9KxE3wJ29
[!]add: 15azScMmHvFPAQfQafrKr48E9MqRRXSnVv
^C] Total 188541952 keys in 30 seconds:  ~6 Mkeys/s (6284731 keys/s)

```
## eth mode

```
./keyhunt -c eth -f tests/1to32.eth -r 111111111:100000000
[+] Version 0.2.230519 Satoshi Quest, developed by AlbertoBSD
[+] Setting search for ETH adddress.
[W] Opps, start range can't be great than end range. Swapping them
[+] N = 0x100000000
[+] Range 
[+] -- from : 0x100000000
[+] -- to   : 0x111111111
[+] Allocating memory for 32 elements: 0.00 MB
[+] Bloom filter for 32 elements.
[+] Loading data to the bloomfilter total: 0.03 MB
[+] Sorting data ... done! 32 values were loaded and sorted
^C] Total 36908032 keys in 30 seconds: ~1 Mkeys/s (1230267 keys/s)



./keyhunt -c eth -f tests/1to32.eth -r 111111111:100000000
[+] Version 1.0 Technical Support: github.com/8891689
[+] Setting search for ETH adddress.
[W] Opps, start range can't be great than end range. Swapping them
[+] N = 0x100000000
[+] Range 
[+] -- from : 0x100000000
[+] -- to   : 0x111111111
[+] Allocating memory for 32 elements: 0.00 MB
[+] Bloom filter for 32 elements.
[+] Loading data to the bloomfilter total: 0.03 MB
[+] Sorting data ... done! 32 values were loaded and sorted
^C] Total 65408000 keys in 30 seconds:  ~2 Mkeys/s (2180266 keys/s)

```

## Thanks

- IceLand
- kanhavishva
- XopMC
- WanderingPhilosopher
- Malboro Man
- NetSec
- Jean Luc Pons
- gemini



# Sponsorship
If this project has been helpful or inspiring, please consider buying me a coffee. Your support is greatly appreciated. Thank you!
```
BTC: bc1qt3nh2e6gjsfkfacnkglt5uqghzvlrr6jahyj2k
ETH: 0xD6503e5994bF46052338a9286Bc43bC1c3811Fa1
DOGE: DTszb9cPALbG9ESNJMFJt4ECqWGRCgucky
TRX: TAHUmjyzg7B3Nndv264zWYUhQ9HUmX4Xu4
```
Thank you.
