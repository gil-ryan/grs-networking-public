# Subnetting

Most engineers uses a [Subnet Calculator](http://www.subnet-calculator.com/subnet.php?net_class=A).

## Slash Notation Chart

|Binary|                             Hex|        Quad Dec|          2ⁿ|    CIDR|   Number of addresses|
|:-:|:-:|:-:|:-:|:-:|:-:|
|00000000000000000000000000000000|   00000000|   0.0.0.0        |   2³²|   /0|     4,294,967,296|     4 G|
|10000000000000000000000000000000|   80000000|   128.0.0.0      |   2³¹|   /1|     2,147,483,648|     2 G|
|11000000000000000000000000000000|   C0000000|   192.0.0.0      |   2³⁰|   /2|     1,073,741,824|     1 G|
|11100000000000000000000000000000|   E0000000|   224.0.0.0      |   2²⁹|   /3|       536,870,912|   512 M|
|11110000000000000000000000000000|   F0000000|   240.0.0.0      |   2²⁸|   /4|       268,435,456|   256 M|
|11111000000000000000000000000000|   F8000000|   248.0.0.0      |   2²⁷|   /5|       134,217,728|   128 M|
|11111100000000000000000000000000|   FC000000|   252.0.0.0      |   2²⁶|   /6|        67,108,864|    64 M|
|11111110000000000000000000000000|   FE000000|   254.0.0.0      |   2²⁵|   /7|        33,554,432|    32 M|
|11111111000000000000000000000000|   FF000000|   255.0.0.0      |   2²⁴|   /8|        16,777,216|    16 M|
|11111111100000000000000000000000|   FF800000|   255.128.0.0    |   2²³|   /9|         8,388,608|     8 M|
|11111111110000000000000000000000|   FFC00000|   255.192.0.0    |   2²²|   /10|        4,194,304|     4 M|
|11111111111000000000000000000000|   FFE00000|   255.224.0.0    |   2²¹|   /11|        2,097,152|     2 M|
|11111111111100000000000000000000|   FFF00000|   255.240.0.0    |   2²⁰|   /12|        1,048,576|     1 M|
|11111111111110000000000000000000|   FFF80000|   255.248.0.0    |   2¹⁹|   /13|          524,288|   512 k|
|11111111111111000000000000000000|   FFFC0000|   255.252.0.0    |   2¹⁸|   /14|          262,144|   256 k|
|11111111111111100000000000000000|   FFFE0000|   255.254.0.0    |   2¹⁷|   /15|          131,072|   128 k|
|11111111111111110000000000000000|   FFFF0000|   255.255.0.0    |   2¹⁶|   /16|           65,536|    64 k|
|11111111111111111000000000000000|   FFFF8000|   255.255.128.0  |   2¹⁵|   /17|           32,768|    32 k|
|11111111111111111100000000000000|   FFFFC000|   255.255.192.0  |   2¹⁴|   /18|           16,384|    16 k|
|11111111111111111110000000000000|   FFFFE000|   255.255.224.0  |   2¹³|   /19|            8,192|     8 k|
|11111111111111111111000000000000|   FFFFF000|   255.255.240.0  |   2¹²|   /20|            4,096|     4 k|
|11111111111111111111100000000000|   FFFFF800|   255.255.248.0  |   2¹¹|   /21|            2,048|     2 k|
|11111111111111111111110000000000|   FFFFFC00|   255.255.252.0  |   2¹⁰|   /22|            1,024|     1 k|
|11111111111111111111111000000000|   FFFFFE00|   255.255.254.0  |   2⁹|    /23|              512|
|11111111111111111111111100000000|   FFFFFF00|   255.255.255.0  |   2⁸|    /24|              256|
|11111111111111111111111110000000|   FFFFFF80|   255.255.255.128|   2⁷|    /25|              128|
|11111111111111111111111111000000|   FFFFFFC0|   255.255.255.192|   2⁶|    /26|               64|
|11111111111111111111111111100000|   FFFFFFE0|   255.255.255.224|   2⁵|    /27|               32|
|11111111111111111111111111110000|   FFFFFFF0|   255.255.255.240|   2⁴|    /28|               16|
|11111111111111111111111111111000|   FFFFFFF8|   255.255.255.248|   2³|    /29|                8|
|11111111111111111111111111111100|   FFFFFFFC|   255.255.255.252|   2²|    /30|                4|
|11111111111111111111111111111110|   FFFFFFFE|   255.255.255.254|   2¹|    /31|                2|
|11111111111111111111111111111111|   FFFFFFFF|   255.255.255.255|   2⁰|    /32|                1|