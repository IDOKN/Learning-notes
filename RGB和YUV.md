###RGB和YUV
关于RGB和YUV网上有各种说明
#####YUV优点
 YUV的原理是把亮度（Y）色度（U和V）分离，从而适合于图像处理领域，如彩色转黑白，通过采样来压缩大小；

研究证明，人眼对亮度的敏感超过色度。利用这个原理，可以把色度信息减少一点，人眼也无法查觉这一点；采样后的YUV数据总尺寸小于RGB格式（4:4:4并没有大小变化，质量很高）。
####采样格式

#####示例YUV 4:4:4
![4:4:4](https://i-msdn.sec.s-msft.com/dynimg/IC130499.gif)

4:2:2
![4:2:2](https://i-msdn.sec.s-msft.com/dynimg/IC84769.gif)
4:2:0
![MPEG-2 scheme](https://i-msdn.sec.s-msft.com/dynimg/IC146945.gif)

等等参考 [msdn介绍YUV](https://msdn.microsoft.com/en-us/library/aa904813%28VS.80%29.aspx)

RGB转YUV：

    //RGB 转换成 YUV
    Y = (0.257 * R) + (0.504 * G) + (0.098 * B) + 16
    Cr = V = (0.439 * R) - (0.368 * G) - (0.071 * B) + 128
    Cb = U = -( 0.148 * R) - (0.291 * G) + (0.439 * B) + 128
    //YUV 转换成 RGB
    B = 1.164(Y - 16) + 2.018(U - 128)
    G = 1.164(Y - 16) - 0.813(V - 128) - 0.391(U - 128)
    R = 1.164(Y - 16) + 1.596(V - 128)
    
    //代码中 RGB转YUV
    Y = ( (  66 * R + 129 * G +  25 * B + 128) >> 8) +  16
	U = ( ( -38 * R -  74 * G + 112 * B + 128) >> 8) + 128
	V = ( ( 112 * R -  94 * G -  18 * B + 128) >> 8) + 128

###相关链接

[msdn介绍YUV，不错的文字](https://msdn.microsoft.com/en-us/library/aa904813%28VS.80%29.aspx)
[知名音视频博客，可惜过世了](http://blog.csdn.net/leixiaohua1020/article/details/18893769)