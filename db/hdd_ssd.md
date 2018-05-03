### HDD 与 SSD 不同存储介质的单片存储大小
##### L0-L1 target file size
- HDD: 192 * 1024 * 1024 = 192M
- SSD: 32 * 1024 * 1024 = 32M

##### L2-LN target file size multiplier
- HDD: 1
- SSD: 2

##### rate limiter for background flushes and compactions, bytes/sec, if any
- HDD: 8 * 1024 * 1024 = 8M
- SSD: None
