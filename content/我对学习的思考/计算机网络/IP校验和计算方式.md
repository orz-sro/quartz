# IP 数据包 checksum 计算


>[!hint] 过程
	头部字节序列
	    │
	    ▼
	每次取2字节拼成16位字
	    │
	    ▼
	反码累加（超出16位的进位回卷加回低位）
	    │
	    ▼
	累加结果取反
	    │
	    ▼
	得到校验和（填入IP头部校验和字段）

### 代码

```c
uint16_t calculate_checksum(uint16_t *header, int len) {
    uint32_t checksum = 0;

    // 用 uint32_t 累加，防止多次相加溢出 16 位
    for (int i = 0; i < len / 2; i++) {
        checksum += header[i];
    }

    // 处理回卷（进位加回低16位）
    while (checksum >> 16) {
        checksum = (checksum & 0xFFFF) + (checksum >> 16);
    }

    // 取反，uint16_t 自动截断
    return ~(uint16_t)checksum;
}
```


