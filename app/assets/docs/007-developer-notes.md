# Peercoin developer notes

Constants that may be useful when looking to integrate / develop with Peercoin.

Peercoin source code repository: github.com/peercoin/peercoin

## mainnet

| Attribute | Value |
|-----------|-------|
| p2pkh Base58 prefix | P |
| p2sh Base58 prefix | p |
| p2pkh Base58 prefix (hex) | 0x37 |
| p2sh Base58 prefix (hex) | 0x75 |
| Magic bytes |  \xe6\xe8\xe9\xe5 |
| WIF prefix | 0xb7 |
| Genesis hash hex (big-endian) |  0000000032fe677166d54963b62a4677d8957e87c508eaa4fd7eb1c880cd27e3 |
| Genesis hash bytes (little-endian) |  \xe3\x27\xcd\x80\xc8\xb1\x7e\xfd\xa4\xea\x08\xc5\x87\x7e\x95\xd8\x77\x46\x2a\xb6\x63\x49\xd5\x66\x71\x67\xfe\x32\x00\x00\x00\x00 |
| Genesis tx hash hex | 3c2d8f85fab4d17aac558cc648a1a58acff0de6deb890c29985690052c5993c2 |
| Genesis tx hash bytes |  \xc2\x93\x59\x2c\x05\x90\x56\x98\x29\x0c\x89\xeb\x6d\xde\xf0\xcf\x8a\xa5\xa1\x48\xc6\x8c\x55\xac\x7a\xd1\xb4\xfa\x85\x8f\x2d\x3c |
| Default port | 9901 |

## testnet

| Attribute | Value |
|-----------|-------|
| p2pkh Base58 prefix | m or n |
| p2sh Base58 prefix | n |
| p2pkh Base58 prefix (hex) | 0x6f |
| p2sh Base58 prefix (hex) | 0xc4 |
| Magic bytes | \xcb\xf2\xc0\xef |
| WIF prefix | 0xef |
| Genesis hash hex (big-endian) | 00000001f757bb737f6596503e17cd17b0658ce630cc727c0cca81aec47c9f06 |
| Genesis hash bytes (little-endian) |  \x06\x9f\x7c\xc4\xae\x81\xca\x0c\x7c\x72\xcc\x30\xe6\x8c\x65\xb0\x17\xcd\x17\x3e\x50\x96\x65\x7f\x73\xbb\x57\xf7\x01\x00\x00\x00  |
| Genesis tx hash hex | 3c2d8f85fab4d17aac558cc648a1a58acff0de6deb890c29985690052c5993c2 |
| Genesis tx hash bytes |  \xc2\x93\x59\x2c\x05\x90\x56\x98\x29\x0c\x89\xeb\x6d\xde\xf0\xcf\x8a\xa5\xa1\x48\xc6\x8c\x55\xac\x7a\xd1\xb4\xfa\x85\x8f\x2d\x3c |
| Default port | 9903 |