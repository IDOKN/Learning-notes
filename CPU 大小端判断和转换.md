###CPU 大小端判断和转换
大端方式将高位存放在低地址，小端方式将低位存放在高地址。采用大端方式 进行数据存放符合人类的正常思维，网络字节序是大端；而采用小端方式进行数据存放利于计算机处理，ARM，x86等 小端（iPhone，Android）。
####示例
32位整数 0x12345678

	地址		  大端		 小端
	0x00		12			78	
	0x01		34			56
	0x02		56			34
	0x03		78			12
####判断

Linux内核判断方法：

    static union { char c[4]; unsigned long mylong; } 
    endian_test = {{'l','?','?','b'}};
    #define ENDIANNESS ((char)endian_test.mylong)
    cout<<ENDIANNESS<<endl;

####大小端转换，其实就是简单的位运算

    typedef unsigned short int uint16;
    typedef unsigned long int uint32;
    #define BigLittleSwap16(A)            ((((uint16)(A) & 0xff00) >> 8) | \
											(((uint16)(A) & 0x00ff) << 8))
    #define BigLittleSwap32(A)            ((((uint32)(A) & 0xff000000) >> 24) | \
                                            (((uint32)(A) & 0x00ff0000) >> 8) | \
                                            (((uint32)(A) & 0x0000ff00) << 8) | \
                                            (((uint32)(A) & 0x000000ff) << 24))

