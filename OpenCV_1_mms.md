# OpenCV_Python🚋

> 写的比较混乱，主要是因为也不知道怎么去概括。。
>
> 而且很多图形和run出来的结果真的需要自己跑一遍才能有体会
>
> 而md文档再上传到GitHub上的话，图片好多传不上去。。（可能是我自己问题
>
> 建议下载一张png图片，然后把文档里面代码的图片地址都换一下
>
> 以上🛹

## 数字图像

通常图像分为单通道、三通道、四通道；

        单通道：也就是通常所说的灰度图，每个像素点只有一个值表示，如果图像的深度是4-(256 = 2*2*2*2)，那么他的像素值0(黑)~255(白)；
    
        三通道：也就是通过见到的彩色图，每个像素点有三个值表示，如果图像深度是4-(256 = 2*2*2*2),那么他的像素值有红(0~255)、绿(0~255)、蓝(0~255)叠加表示，色彩更加艳丽;
    
        四通道：也就是在三通道图像基础上加上透明程度，Alpha色彩空间，如果图像深度是4-(256 = 2*2*2*2),那么0是完全透明，255是完全不透明；





## 上代码

### 图像色彩

```python
import cv2 as cv


def read_demo():
    image = cv.imread("C:/Users/26368/Desktop/pngtest.png")
    cv.imshow("input", image)
    cv.waitKey(0)
    cv.destroyAllWindows()


def color_space_demo():
    image = cv.imread("C:/Users/26368/Desktop/pngtest.png")
    gray = cv.cvtColor(image, cv.COLOR_BGR2GRAY)
    hsv = cv.cvtColor(image, cv.COLOR_BGR2HSV)
    cv.imshow("gray", gray)  #cout
    cv.imshow("hsv", hsv)
    cv.waitKey(0)#不断刷新图像,如果是0就一直显示，如果是其他数字就展示多少毫秒
    cv.destroyAllWindows()


if __name__ == "__main__":#类似于int main()
    read_demo()#关闭窗口之后才会显示下一条语句
    color_space_demo()
```

waitKey(delay )在一个给定的时间内(单位ms)等待用户按键触发;如果用户没有按下键,则继续等待(循环)。有按键按下，返回按键的ASCII值。无按键按下，返回-1。

延时delay = 0 函数则延时无限长，必须有键按下才继续执行。
延时delay > 0 函数返回值为按下的键的ASCII码值，超时则返回-1。
waitKey(0),表示程序会无限制的等待用户的按键事件；
waitKey(1),表示程序每1ms检测一次按键，检测到返回按键值，检测不到返回-1；
waitKey(100),表示程序每100ms检测一次按键，检测到返回按键值，检测不到返回-1；





### 图像裁剪

```python
import cv2 as cv
import numpy as np


def mat_demo():
    image = cv.imread("C:/Users/26368/Desktop/pngtest.png")
    print(image.shape)  # 出来 高度h，宽度w，通道数c
    h, w, c = image.shape
    # 要导入import numpy as np
    roi = image[100:200, 100:200, :]
    blank = np.zeros_like(image)  # 创建一个空白图像
    blank_1 = np.zeros((h, w, c), dtype=np.uint8)
    #上面两句话等价
    blank = np.copy(image)
    # 和blank=copy的不同在于，上者复制完后两者就没有关系了，但是左边那个是一种“捆绑”，只要一个修改了另一个就要修改
    blank_1[100:200, 300:400, :] = image[150:250, 350:450, :]
    #最后的,: 可以去掉
    # #100:200是x方向，300:400是y方向，等号两边长度/宽度要一模一样，否则报错
    cv.imshow("image", image)
    cv.imshow("blank", blank)
    cv.imshow("blank_1", blank_1)
    cv.imshow("roi", roi)
    cv.waitKey(0)
    cv.destroyAllWindows()


if __name__ == "__main__":
    mat_demo()
```

一切的图像都是数据



### 取反

```python
import cv2 as cv


def mat_demo():
    # 对每个像素取反
    image = cv.imread("C:/Users/26368/Desktop/pngtest.png")
    print(image.shape)  # 出来 高度h，宽度w，通道数c
    h, w, c = image.shape
    for row in range(h):
        for col in range(w):
            b, g, r = image[row, col]
            #顺序为：蓝色。绿色，红色
            image[row, col] = (255 - b, 255 - g, 255 - r)
    cv.imshow("取反", image)
    cv.waitKey(0)
    cv.destroyAllWindows()


if __name__ == "__main__":
    mat_demo()
```



### 算术操作

```python
import cv2 as cv
import numpy as np


def math_demo():
    image = cv.imread("C:/Users/26368/Desktop/pngtest.png")
    h, w, c = image.shape
    blank = np.zeros_like(image)

    blank[:, :] = (50, 50, 50)
    result_add = cv.add(image, blank)  # 调亮

    blank[:, :] = (50, 50, 50)
    result_subtract = cv.subtract(image, blank)  # 调暗

    blank[:, :] = (2, 2, 2)
    result_multiply = cv.multiply(image, blank)  # 提高对比度

    blank[:, :] = (2, 2, 2)
    result_divide = cv.divide(image, blank)  # 降低对比度

    cv.imshow("origin", image)
    cv.imshow("+", result_add)
    cv.imshow("-", result_subtract)
    cv.imshow("*", result_multiply)
    cv.imshow("/", result_divide)

    cv.waitKey(0)
    cv.destroyAllWindows()


if __name__ == "__main__":
    math_demo()
```



### 滚动条_调整图像亮度

```python
import cv2 as cv
import numpy as np


def nothing(x):
    print(x)


def adjustlightness_demo():
    image = cv.imread("C:/Users/26368/Desktop/pngtest.png")
    cv.namedWindow("input", cv.WINDOW_NORMAL)  # 新建一个显示窗口
    # 参数1：新建的窗口的名称。自己随便取。
    # 参数2：窗口的标识，一般默认为WINDOW_AUTOSIZE
    #     WINDOW_AUTOSIZE：窗口大小自动适应图片大小，并且不可手动更改
    #     WINDOW_NORMAL：用户可以改变这个窗口大小
    #     WINDOW_OPENGL：窗口创建的时候会支持OpenGL

    cv.createTrackbar("lightness", "input", 0, 100, nothing)
    # createTrackbar是Opencv中的API，其可在显示图像的窗口中快速创建一个滑动控件，用于手动调节阈值
    # 参数1：trackbarname：滑动空间的名称
    # 参数2：winname：滑动空间用于依附的图像窗口的名称，必须和cvNameWindow的参数1完全一致
    # 参数3：value：初始化阈值
    # 参数4：count：滑动控件的刻度范围
    # 参数5：TrackbarCallback是回调函数，这里就简单定义成了nothing这个print函数

    cv.imshow("input", image)
    blank = np.zeros_like(image)
    while True:
        pos = cv.getTrackbarPos("lightness", "input")  # 获取当前轨迹条的位置（轨道条名字，窗口名字）
        blank[:, :] = (pos, pos, pos)
        result = cv.add(image, blank)
        cv.imshow("result", result)
        c = cv.waitKey(1)  # 每1ms就检测一次，c为按下键的Ascll代码，比如Esc为27，如果没有按键，则返回-1
        if c == 27:
            break
    cv.destroyAllWindows()


if __name__ == "__main__":
    adjustlightness_demo()
```





### 滚动条_调整亮度和对比度

```python
import cv2 as cv
import numpy as np


def nothing(x):
    print(x)


def adjust_contrast_demo():
    image = cv.imread("C:/Users/26368/Desktop/pngtest.png")
    cv.namedWindow("input", cv.WINDOW_AUTOSIZE)
    cv.createTrackbar("lightness", "input", 0, 100, nothing)
    cv.createTrackbar("contrast", "input", 0, 200, nothing)
    cv.imshow("input", image)
    blank = np.zeros_like(image)
    print(blank)
    while True:
        light = cv.getTrackbarPos("lightness", "input")
        contrast = cv.getTrackbarPos("contrast", "input") / 100
        result = cv.addWeighted(image, contrast, blank, 0.5, light)
        # void addWeighted(InputArray src1, double alpha, InputArray src2, double beta, double gamma, OutputArray dst, int dtype = -1)
        # 参数1：src1，第一张图.
        # 参数2：alpha，第一张图要乘的
        # 参数3：src2第二张图
        # 参数4：beta，第二张图要乘的
        # 参数5：gamma，图1与图2作和后添加的数值
        # dst = src1[i] * alpha + src2 * beta + gamma;
        #
        # 参数6：dst，输出图片。默认值为-1，可以不写

        c = cv.waitKey(1)
        if c == 27:
            break
    cv.destroyAllWindows()


if __name__ == "__main__":
    adjust_contrast_demo()
```





### 键盘响应

```python
import cv2 as cv


def keys_demo():
    image = cv.imread("C:/Users/26368/Desktop/pngtest.png")
    cv.namedWindow("input", cv.WINDOW_AUTOSIZE)
    cv.imshow("input", image)
    while True:
        c=cv.waitKey(1)
        if c==49:
            gray=cv.cvtColor(image,cv.COLOR_BGR2GRAY)
            cv.imshow("result",gray)
        if c==50:
            hsv=cv.cvtColor(image,cv.COLOR_BGR2HSV)
            cv.imshow("result",hsv)
        if c==27:
            break

    while True:
        c = cv.waitKey(1000)
        gray = image
        if c == 49:
            gray = cv.cvtColor(image, cv.COLOR_BGR2GRAY)
        if c == 50:
            gray = cv.cvtColor(image, cv.COLOR_BGR2HSV)
        cv.imshow("result", gray)
        if c == 27:
            break

    cv.destroyAllWindows()


if __name__ == "__main__":
    keys_demo()
```



```python
import cv2 as cv
import numpy as np


def nothing(x):
    print(x)


def color_table_demo():
    colormap = [
                   cv.COLORMAP_AUTUMN,
                   cv.COLORMAP_BONE,
                   cv.COLORMAP_JET,
                   cv.COLORMAP_OCEAN,
                   cv.COLORMAP_PINK,
               ]
    image = cv.imread("C:/Users/26368/Desktop/pngtest.png")
    cv.namedWindow("input", cv.WINDOW_AUTOSIZE)
    cv.imshow("input", image)
    index = 0
    while True:
        dst = cv.applyColorMap(image, colormap[index % 5])
        index += 1
        cv.imshow("color style", dst)
        c = cv.waitKey(500)
        if c == 27:
            break
    cv.destroyAllWindows()


if __name__ == "__main__":
    color_table_demo()
```





### 图像像素的逻辑操作

注意别把zero打成zeor

uint8别打成unit8

```python
import cv2 as cv
import numpy as np


def bitwise_demo():
    b1 = np.zeros((200, 400, 3), dtype=np.uint8)#200是高，400是长
    b1[:, :] = (0, 0, 255)
    b2 = np.zeros((200, 400, 3), dtype=np.uint8)
    b2[:, :] = (0, 255, 0)
    cv.imshow("b1", b1)
    cv.imshow("b2", b2)
    dst1 = cv.bitwise_and(b1, b2)
    dst2 = cv.bitwise_or(b1, b2)
    # bitwise_and是对二进制数据进行“与”操作，即对图像（灰度图像或彩色图像均可）每个像素值进行二进制“与”操作
    # 1 & 1 = 1，1 & 0 = 0，0 & 1 = 0，0 & 0 = 0
    # bitwise_or是对二进制数据进行“或”操作，即对图像（灰度图像或彩色图像均可）每个像素值进行二进制“或”操作
    # 1 | 1 = 1，1 | 0 = 0，0 | 1 = 0，0 | 0 = 0
    # bitwise_xor是对二进制数据进行“异或”操作，即对图像（灰度图像或彩色图像均可）每个像素值进行二进制“异或”操作
    # 1 ^ 1 = 0, 1 ^ 0 = 1, 0 ^ 1 = 1, 0 ^ 0 = 0
    # bitwise_not是对二进制数据进行“非”操作，即对图像（灰度图像或彩色图像均可）每个像素值进行二进制“非”操作
    # ~1 = 0，~0 = 1
    cv.imshow("bitwise_and", dst1)
    cv.imshow("bitwise_or", dst2)
    cv.waitKey(0)
    cv.destroyAllWindows()


if __name__ == "__main__":
    bitwise_demo()
```

img[:,:,::-1]也就是我们任意不改变width维的方式，也不改变height维的方式，仅仅改变channel维的方式，并且是倒序排列，原本的bgr排列方式经过倒序就变成了rgb的通道排列方式。

img[::-1, :, :]是对图片进行上下翻转

 img[:,::-1,:]是对图像进行左右翻转

numpy索引







### 通道分离与合并

```python
import cv2 as cv
import numpy as np


def bitwise_demo():
    b1 = cv.imread("C:/Users/26368/Desktop/pngtest.png")
    cv.imshow("input", b1)
    cv.imshow("0", b1[:, :, 0])
    cv.imshow("-1", b1[:, :, -1])
    cv.imshow("2", b1[:, :, 2])
    cv.waitKey(0)
    cv.destroyAllWindows()


if __name__ == "__main__":
    bitwise_demo()

```

### cv2.split() 的函数使用

图像颜色通道的分离：

```
import numpy as np
import cv2             


# 读取要处理的图片
image = cv2.imread(".../default.png") 

# 分离出图片的 B，R，G 颜色通道           
B, G, R = cv2.split(image)  

# 显示三通道的值都为 R 值时的图片                       
cv2.imshow("RED", R) 

# 显示三通道的值都为 G 值时的图片                          
cv2.imshow("GREEN", G)                 

# 显示三通道的值都为 B 值时的图片           
cv2.imshow("BLUE", B)  

# 不让程序突然结束                           
cv2.waitKey(0)
```

执行上述程序后。得到三张不同的灰度图：

为什么得到的是三张不同的灰度图呢？不是已经分离出 R，G，B 通道了吗？应该是分别是红色图，绿色图，蓝色图才对啊。

原因是：当调用 imshow(R) 时，是把图像的 R，G，B 三个通道的值都变为 R 的值，所以图像的颜色三通道值为（R，R，R）

同理 imshow(G) 和 imshow(B) 所显示的图像的颜色通道也依次为（G，G，G）和（B，B，B）。

而当三个通道的值相同时，则为灰度图。

有人可能会问，不是 R，G，B 吗，为什么 B 通道反而放在图像的第一位，如（B，0，0）？

因为 opencv 中，就是调过来的，图像的第一通道是 B，第二通道是 G，最后是 R。

下面将使用 merge() 函数将某一颜色通道（如 R）与零矩阵合并，形成（R，0，0）从而显示只有红色通道的图



### cv.merge() 函数的使用

```python
import numpy as np
import cv2     

# 读取要处理的图片
image=cv2.imread(".../default.png")

# 分离出图片的 B，R，G 颜色通道
B, G, R = cv2.split(image)    

# 创建与 image 相同大小的零矩阵
zeros = np.zeros(image.shape[:2], dtype="uint8")

# 显示（0，0，R）图像
cv2.imshow("RED",cv2.merge([zeros, zeros, R]))

# 显示（0，G，0）图像
cv2.imshow("GREEN",cv2.merge([zeros, G, zeros]))

# 显示 （B，0，0）图像
cv2.imshow("BLUE",cv2.merge([B, zeros, zeros]))

cv2.waitKey(0)
```

运行结果会分别显示三张图

我们最后尝试把 分离出来的 R，G，B 通道的值重新合并在一起，看是否能获得原图：

```python
import numpy as np
import cv2


# 读取要处理的图片
image=cv2.imread(".../default.png")

# 分离出图片的 B，R，G 颜色通道
B, G, R = cv2.split(image)

# 创建与 image 相同大小的零矩阵
zeros = np.zeros(image.shape[:2], dtype="uint8")

cv2.imshow("MERGE", cv2.merge([B, G, R]))

cv2.waitKey(0)
```

结果获得原图



视频里面的代码（不是很懂

```python
import cv2 as cv
import numpy as np


def bitwise_demo():
    b1 = cv.imread("C:/Users/26368/Desktop/pngtest.png")
    print(b1.shape)
    cv.imshow("input",b1)
    cv.imshow("b1",b1[:,:,2])
    mv=cv.split(b1)#mv也可以换成B,G,R——分别为分离出来的图片的B，R，G 颜色通道
    mv[2][:,:]=255
    result=cv.merge(mv)
    cv.imshow("result",result)
    cv.waitKey(0)
    cv.destroyAllWindows()


if __name__ == "__main__":
    bitwise_demo()
```



### 图像色彩空间转换

（把绿色提取出来）

```python
import cv2 as cv
import numpy as np


def bitwise_demo():
    b1 = cv.imread("C:/Users/26368/Desktop/pngtest.png")
    print(b1.shape)
    cv.imshow("input", b1)
    hsv = cv.cvtColor(b1, cv.COLOR_BGR2HSV)
    cv.imshow("hsv", hsv)
    mask = cv.inRange(hsv, (35, 43, 46), (77, 255, 255))
    #mask = cv.inRange(hsv, (20, 20, 20), (200, 200, 200))
    cv.bitwise_and(b1, b1, mask=mask)
    cv.imshow("mask", mask)
    cv.bitwise_not(mask,mask)
    result=cv.bitwise_and(b1,b1,mask=mask)
    cv.imshow("result",result)
    cv.waitKey(0)
    cv.destroyAllWindows()


if __name__ == "__main__":
    bitwise_demo()

```

![img](https://img-blog.csdnimg.cn/20191029100153461.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2h1YW5nX25hbnNlbg==,size_16,color_FFFFFF,t_70)





### 图像像素值统计

mean：输出参数，计算均值

stddev：输出参数，计算标准差

```python
import cv2 as cv
import numpy as np


def demo():
    b1 = cv.imread("C:/Users/26368/Desktop/pngtest.png")
    print('\n', b1.shape)
    cv.imshow("input", b1)
    means, dev = cv.meanStdDev(b1)
    print('\n', means)
    print('\n',"dev:", dev)
    cv.waitKey(0)
    cv.destroyAllWindows()


if __name__ == "__main__":
    demo()

```





### 图形几何形状绘制

```python
import cv2 as cv
import numpy as np


def demo():
    b1 = cv.imread("C:/Users/26368/Desktop/peoplepng.png")
    #temp=np.copy(b1)
    cv.rectangle(b1,(5,5),(690,650),(0,0,255),4,8,0)
    #(5,5)是左上角的坐标，（690,650）是右下角坐标，（0,0,255）是颜色(RGB)，int thickness=4(如果是负数就实心，如果是0的话还是会有线), int lineType=8, int shift=0
    # thickness:线条的粗细程度。取负值时（如 CV_FILLED）函数绘制填充了色彩的矩形。
    # line_type:线条的类型。见cvLine的描述
    # shift:坐标点的小数点位数
    cv.circle(b1,(300,300),350,(0,255,255),4,8,0)
    #(300,300)圆心坐标 350半径
    cv.line(b1,(30,30),(300,300),(0,255,255),4,8,0)
    cv.putText(b1,"99%face",(50,50),cv.FONT_HERSHEY_SIMPLEX,1.0,(0,255,255),2,8)
    # 在图像上绘制文字
    # void cv.putText(待绘制的图像,文字,文本框左下角的坐标,字体(如cv::FONT_HERSHEY_PLAIN),尺寸(值越大文字越大),颜色（RGB）
    # int thickness线条宽度,lineType = 8, 线型（4邻域或8邻域，默认8邻域）,bool bottomLeftOrigin :为True时图像文字翻转,默认为0)

    cv.imshow("input",b1)
    cv.waitKey(0)
    cv.destroyAllWindows()


if __name__ == "__main__":
    demo()

```



### 随机数和随机颜色

```python
import cv2 as cv
import numpy as np


def demo():
    b1 = np.zeros((512, 512, 3), dtype=np.uint8)
    while True:
        xx = np.random.randint(0, 512, 2, dtype=np.int)
        # numpy.random.randint(low, high=None, size=None, dtype='l'如int64、int)
        # 返回一个随机整型数，范围从低（包括）到高（不包括），即[low, high)。
        # 如果没有写参数high的值，则返回[0, low)的值。
        # size:输出随机数的尺寸，比如size = (m * n * k),这里返回的是二维数组
        # 则输出同规模即m * n * k个随机数。默认是None的，仅仅返回满足要求的单一随机数。
        yy = np.random.randint(0, 512, 2, dtype=np.int)
        bgr = np.random.randint(0, 255, 3, dtype=np.int)
        print(bgr[0],bgr[1],bgr[2])
        cv.line(b1,(xx[0],yy[0]),(xx[1],yy[1]),(np.int(bgr[0]),np.int(bgr[1]),np.int(bgr[2])),2,8,0)
        cv.imshow("input",b1)
        c=cv.waitKey(10)
        if c==27:
            break
    cv.destroyAllWindows()


if __name__ == "__main__":
    demo()

```





### 多边形填充与绘制

```python
import cv2 as cv
import numpy as np


def demo():
    canvas = np.zeros((512, 512, 3), dtype=np.uint8)
    pts = np.array([[100, 100], [350, 100], [450, 280], [
                   320, 450], [80, 400], [30, 300]], dtype=np.int32)

    cv.fillPoly(canvas, [pts], (0, 0, 255), 8, 0)

    # cv.polylines(canvas,[pts],True,(0,0,255),2,8,0)
    # void cv.PolyLine(图像, CvPoint ** pts（折线的顶点指针数组）,int is_closed（指出多边形是否封闭。如果封闭，函数将起始点和结束点连线）,
    # 颜色, int thickness = 1, int line_type = 8（线段的类型。参见cvLine）, int shift = 0（顶点的小数点位数）)

    # cv.drawContours(canvas, [pts], -1, (255, 0, 0),4)
    # -1是 int contourIdx, // 需要绘制的轮廓的指数 (-1 表示 "all")
    # 4是宽度
    cv.imshow("new", canvas)
    cv.waitKey(0)
    cv.destroyAllWindows()


if __name__ == "__main__":
    demo()

```

