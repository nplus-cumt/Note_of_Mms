# OpenCV_Pythonð

> åçæ¯è¾æ··ä¹±ï¼ä¸»è¦æ¯å ä¸ºä¹ä¸ç¥éæä¹å»æ¦æ¬ãã
>
> èä¸å¾å¤å¾å½¢årunåºæ¥çç»æççéè¦èªå·±è·ä¸éæè½æä½ä¼
>
> èmdææ¡£åä¸ä¼ å°GitHubä¸çè¯ï¼å¾çå¥½å¤ä¼ ä¸ä¸å»ããï¼å¯è½æ¯æèªå·±é®é¢
>
> å»ºè®®ä¸è½½ä¸å¼ pngå¾çï¼ç¶åæææ¡£éé¢ä»£ç çå¾çå°åé½æ¢ä¸ä¸
>
> ä»¥ä¸ð¹

## æ°å­å¾å

éå¸¸å¾ååä¸ºåééãä¸ééãåééï¼

        åééï¼ä¹å°±æ¯éå¸¸æè¯´çç°åº¦å¾ï¼æ¯ä¸ªåç´ ç¹åªæä¸ä¸ªå¼è¡¨ç¤ºï¼å¦æå¾åçæ·±åº¦æ¯4-(256 = 2*2*2*2)ï¼é£ä¹ä»çåç´ å¼0(é»)~255(ç½)ï¼
    
        ä¸ééï¼ä¹å°±æ¯éè¿è§å°çå½©è²å¾ï¼æ¯ä¸ªåç´ ç¹æä¸ä¸ªå¼è¡¨ç¤ºï¼å¦æå¾åæ·±åº¦æ¯4-(256 = 2*2*2*2),é£ä¹ä»çåç´ å¼æçº¢(0~255)ãç»¿(0~255)ãè(0~255)å å è¡¨ç¤ºï¼è²å½©æ´å è³ä¸½;
    
        åééï¼ä¹å°±æ¯å¨ä¸ééå¾ååºç¡ä¸å ä¸éæç¨åº¦ï¼Alphaè²å½©ç©ºé´ï¼å¦æå¾åæ·±åº¦æ¯4-(256 = 2*2*2*2),é£ä¹0æ¯å®å¨éæï¼255æ¯å®å¨ä¸éæï¼





## ä¸ä»£ç 

### å¾åè²å½©

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
    cv.waitKey(0)#ä¸æ­å·æ°å¾å,å¦ææ¯0å°±ä¸ç´æ¾ç¤ºï¼å¦ææ¯å¶ä»æ°å­å°±å±ç¤ºå¤å°æ¯«ç§
    cv.destroyAllWindows()


if __name__ == "__main__":#ç±»ä¼¼äºint main()
    read_demo()#å³é­çªå£ä¹åæä¼æ¾ç¤ºä¸ä¸æ¡è¯­å¥
    color_space_demo()
```

waitKey(delay )å¨ä¸ä¸ªç»å®çæ¶é´å(åä½ms)ç­å¾ç¨æ·æé®è§¦å;å¦æç¨æ·æ²¡ææä¸é®,åç»§ç»­ç­å¾(å¾ªç¯)ãææé®æä¸ï¼è¿åæé®çASCIIå¼ãæ æé®æä¸ï¼è¿å-1ã

å»¶æ¶delay = 0 å½æ°åå»¶æ¶æ éé¿ï¼å¿é¡»æé®æä¸æç»§ç»­æ§è¡ã
å»¶æ¶delay > 0 å½æ°è¿åå¼ä¸ºæä¸çé®çASCIIç å¼ï¼è¶æ¶åè¿å-1ã
waitKey(0),è¡¨ç¤ºç¨åºä¼æ éå¶çç­å¾ç¨æ·çæé®äºä»¶ï¼
waitKey(1),è¡¨ç¤ºç¨åºæ¯1msæ£æµä¸æ¬¡æé®ï¼æ£æµå°è¿åæé®å¼ï¼æ£æµä¸å°è¿å-1ï¼
waitKey(100),è¡¨ç¤ºç¨åºæ¯100msæ£æµä¸æ¬¡æé®ï¼æ£æµå°è¿åæé®å¼ï¼æ£æµä¸å°è¿å-1ï¼





### å¾åè£åª

```python
import cv2 as cv
import numpy as np


def mat_demo():
    image = cv.imread("C:/Users/26368/Desktop/pngtest.png")
    print(image.shape)  # åºæ¥ é«åº¦hï¼å®½åº¦wï¼ééæ°c
    h, w, c = image.shape
    # è¦å¯¼å¥import numpy as np
    roi = image[100:200, 100:200, :]
    blank = np.zeros_like(image)  # åå»ºä¸ä¸ªç©ºç½å¾å
    blank_1 = np.zeros((h, w, c), dtype=np.uint8)
    #ä¸é¢ä¸¤å¥è¯ç­ä»·
    blank = np.copy(image)
    # åblank=copyçä¸åå¨äºï¼ä¸èå¤å¶å®åä¸¤èå°±æ²¡æå³ç³»äºï¼ä½æ¯å·¦è¾¹é£ä¸ªæ¯ä¸ç§âæç»âï¼åªè¦ä¸ä¸ªä¿®æ¹äºå¦ä¸ä¸ªå°±è¦ä¿®æ¹
    blank_1[100:200, 300:400, :] = image[150:250, 350:450, :]
    #æåç,: å¯ä»¥å»æ
    # #100:200æ¯xæ¹åï¼300:400æ¯yæ¹åï¼ç­å·ä¸¤è¾¹é¿åº¦/å®½åº¦è¦ä¸æ¨¡ä¸æ ·ï¼å¦åæ¥é
    cv.imshow("image", image)
    cv.imshow("blank", blank)
    cv.imshow("blank_1", blank_1)
    cv.imshow("roi", roi)
    cv.waitKey(0)
    cv.destroyAllWindows()


if __name__ == "__main__":
    mat_demo()
```

ä¸åçå¾åé½æ¯æ°æ®



### åå

```python
import cv2 as cv


def mat_demo():
    # å¯¹æ¯ä¸ªåç´ åå
    image = cv.imread("C:/Users/26368/Desktop/pngtest.png")
    print(image.shape)  # åºæ¥ é«åº¦hï¼å®½åº¦wï¼ééæ°c
    h, w, c = image.shape
    for row in range(h):
        for col in range(w):
            b, g, r = image[row, col]
            #é¡ºåºä¸ºï¼èè²ãç»¿è²ï¼çº¢è²
            image[row, col] = (255 - b, 255 - g, 255 - r)
    cv.imshow("åå", image)
    cv.waitKey(0)
    cv.destroyAllWindows()


if __name__ == "__main__":
    mat_demo()
```



### ç®æ¯æä½

```python
import cv2 as cv
import numpy as np


def math_demo():
    image = cv.imread("C:/Users/26368/Desktop/pngtest.png")
    h, w, c = image.shape
    blank = np.zeros_like(image)

    blank[:, :] = (50, 50, 50)
    result_add = cv.add(image, blank)  # è°äº®

    blank[:, :] = (50, 50, 50)
    result_subtract = cv.subtract(image, blank)  # è°æ

    blank[:, :] = (2, 2, 2)
    result_multiply = cv.multiply(image, blank)  # æé«å¯¹æ¯åº¦

    blank[:, :] = (2, 2, 2)
    result_divide = cv.divide(image, blank)  # éä½å¯¹æ¯åº¦

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



### æ»å¨æ¡_è°æ´å¾åäº®åº¦

```python
import cv2 as cv
import numpy as np


def nothing(x):
    print(x)


def adjustlightness_demo():
    image = cv.imread("C:/Users/26368/Desktop/pngtest.png")
    cv.namedWindow("input", cv.WINDOW_NORMAL)  # æ°å»ºä¸ä¸ªæ¾ç¤ºçªå£
    # åæ°1ï¼æ°å»ºççªå£çåç§°ãèªå·±éä¾¿åã
    # åæ°2ï¼çªå£çæ è¯ï¼ä¸è¬é»è®¤ä¸ºWINDOW_AUTOSIZE
    #     WINDOW_AUTOSIZEï¼çªå£å¤§å°èªå¨éåºå¾çå¤§å°ï¼å¹¶ä¸ä¸å¯æå¨æ´æ¹
    #     WINDOW_NORMALï¼ç¨æ·å¯ä»¥æ¹åè¿ä¸ªçªå£å¤§å°
    #     WINDOW_OPENGLï¼çªå£åå»ºçæ¶åä¼æ¯æOpenGL

    cv.createTrackbar("lightness", "input", 0, 100, nothing)
    # createTrackbaræ¯Opencvä¸­çAPIï¼å¶å¯å¨æ¾ç¤ºå¾åççªå£ä¸­å¿«éåå»ºä¸ä¸ªæ»å¨æ§ä»¶ï¼ç¨äºæå¨è°èéå¼
    # åæ°1ï¼trackbarnameï¼æ»å¨ç©ºé´çåç§°
    # åæ°2ï¼winnameï¼æ»å¨ç©ºé´ç¨äºä¾éçå¾åçªå£çåç§°ï¼å¿é¡»åcvNameWindowçåæ°1å®å¨ä¸è´
    # åæ°3ï¼valueï¼åå§åéå¼
    # åæ°4ï¼countï¼æ»å¨æ§ä»¶çå»åº¦èå´
    # åæ°5ï¼TrackbarCallbackæ¯åè°å½æ°ï¼è¿éå°±ç®åå®ä¹æäºnothingè¿ä¸ªprintå½æ°

    cv.imshow("input", image)
    blank = np.zeros_like(image)
    while True:
        pos = cv.getTrackbarPos("lightness", "input")  # è·åå½åè½¨è¿¹æ¡çä½ç½®ï¼è½¨éæ¡åå­ï¼çªå£åå­ï¼
        blank[:, :] = (pos, pos, pos)
        result = cv.add(image, blank)
        cv.imshow("result", result)
        c = cv.waitKey(1)  # æ¯1mså°±æ£æµä¸æ¬¡ï¼cä¸ºæä¸é®çAscllä»£ç ï¼æ¯å¦Escä¸º27ï¼å¦ææ²¡ææé®ï¼åè¿å-1
        if c == 27:
            break
    cv.destroyAllWindows()


if __name__ == "__main__":
    adjustlightness_demo()
```





### æ»å¨æ¡_è°æ´äº®åº¦åå¯¹æ¯åº¦

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
        # åæ°1ï¼src1ï¼ç¬¬ä¸å¼ å¾.
        # åæ°2ï¼alphaï¼ç¬¬ä¸å¼ å¾è¦ä¹ç
        # åæ°3ï¼src2ç¬¬äºå¼ å¾
        # åæ°4ï¼betaï¼ç¬¬äºå¼ å¾è¦ä¹ç
        # åæ°5ï¼gammaï¼å¾1ä¸å¾2ä½ååæ·»å çæ°å¼
        # dst = src1[i] * alpha + src2 * beta + gamma;
        #
        # åæ°6ï¼dstï¼è¾åºå¾çãé»è®¤å¼ä¸º-1ï¼å¯ä»¥ä¸å

        c = cv.waitKey(1)
        if c == 27:
            break
    cv.destroyAllWindows()


if __name__ == "__main__":
    adjust_contrast_demo()
```





### é®çååº

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





### å¾ååç´ çé»è¾æä½

æ³¨æå«æzeroææzeor

uint8å«ææunit8

```python
import cv2 as cv
import numpy as np


def bitwise_demo():
    b1 = np.zeros((200, 400, 3), dtype=np.uint8)#200æ¯é«ï¼400æ¯é¿
    b1[:, :] = (0, 0, 255)
    b2 = np.zeros((200, 400, 3), dtype=np.uint8)
    b2[:, :] = (0, 255, 0)
    cv.imshow("b1", b1)
    cv.imshow("b2", b2)
    dst1 = cv.bitwise_and(b1, b2)
    dst2 = cv.bitwise_or(b1, b2)
    # bitwise_andæ¯å¯¹äºè¿å¶æ°æ®è¿è¡âä¸âæä½ï¼å³å¯¹å¾åï¼ç°åº¦å¾åæå½©è²å¾ååå¯ï¼æ¯ä¸ªåç´ å¼è¿è¡äºè¿å¶âä¸âæä½
    # 1 & 1 = 1ï¼1 & 0 = 0ï¼0 & 1 = 0ï¼0 & 0 = 0
    # bitwise_oræ¯å¯¹äºè¿å¶æ°æ®è¿è¡âæâæä½ï¼å³å¯¹å¾åï¼ç°åº¦å¾åæå½©è²å¾ååå¯ï¼æ¯ä¸ªåç´ å¼è¿è¡äºè¿å¶âæâæä½
    # 1 | 1 = 1ï¼1 | 0 = 0ï¼0 | 1 = 0ï¼0 | 0 = 0
    # bitwise_xoræ¯å¯¹äºè¿å¶æ°æ®è¿è¡âå¼æâæä½ï¼å³å¯¹å¾åï¼ç°åº¦å¾åæå½©è²å¾ååå¯ï¼æ¯ä¸ªåç´ å¼è¿è¡äºè¿å¶âå¼æâæä½
    # 1 ^ 1 = 0, 1 ^ 0 = 1, 0 ^ 1 = 1, 0 ^ 0 = 0
    # bitwise_notæ¯å¯¹äºè¿å¶æ°æ®è¿è¡âéâæä½ï¼å³å¯¹å¾åï¼ç°åº¦å¾åæå½©è²å¾ååå¯ï¼æ¯ä¸ªåç´ å¼è¿è¡äºè¿å¶âéâæä½
    # ~1 = 0ï¼~0 = 1
    cv.imshow("bitwise_and", dst1)
    cv.imshow("bitwise_or", dst2)
    cv.waitKey(0)
    cv.destroyAllWindows()


if __name__ == "__main__":
    bitwise_demo()
```

img[:,:,::-1]ä¹å°±æ¯æä»¬ä»»æä¸æ¹åwidthç»´çæ¹å¼ï¼ä¹ä¸æ¹åheightç»´çæ¹å¼ï¼ä»ä»æ¹åchannelç»´çæ¹å¼ï¼å¹¶ä¸æ¯ååºæåï¼åæ¬çbgræåæ¹å¼ç»è¿ååºå°±åæäºrgbçééæåæ¹å¼ã

img[::-1, :, :]æ¯å¯¹å¾çè¿è¡ä¸ä¸ç¿»è½¬

 img[:,::-1,:]æ¯å¯¹å¾åè¿è¡å·¦å³ç¿»è½¬

numpyç´¢å¼







### ééåç¦»ä¸åå¹¶

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

### cv2.split() çå½æ°ä½¿ç¨

å¾åé¢è²ééçåç¦»ï¼

```
import numpy as np
import cv2             


# è¯»åè¦å¤ççå¾ç
image = cv2.imread(".../default.png") 

# åç¦»åºå¾çç Bï¼Rï¼G é¢è²éé           
B, G, R = cv2.split(image)  

# æ¾ç¤ºä¸ééçå¼é½ä¸º R å¼æ¶çå¾ç                       
cv2.imshow("RED", R) 

# æ¾ç¤ºä¸ééçå¼é½ä¸º G å¼æ¶çå¾ç                          
cv2.imshow("GREEN", G)                 

# æ¾ç¤ºä¸ééçå¼é½ä¸º B å¼æ¶çå¾ç           
cv2.imshow("BLUE", B)  

# ä¸è®©ç¨åºçªç¶ç»æ                           
cv2.waitKey(0)
```

æ§è¡ä¸è¿°ç¨åºåãå¾å°ä¸å¼ ä¸åçç°åº¦å¾ï¼

ä¸ºä»ä¹å¾å°çæ¯ä¸å¼ ä¸åçç°åº¦å¾å¢ï¼ä¸æ¯å·²ç»åç¦»åº Rï¼Gï¼B ééäºåï¼åºè¯¥æ¯åå«æ¯çº¢è²å¾ï¼ç»¿è²å¾ï¼èè²å¾æå¯¹åã

åå æ¯ï¼å½è°ç¨ imshow(R) æ¶ï¼æ¯æå¾åç Rï¼Gï¼B ä¸ä¸ªééçå¼é½åä¸º R çå¼ï¼æä»¥å¾åçé¢è²ä¸ééå¼ä¸ºï¼Rï¼Rï¼Rï¼

åç imshow(G) å imshow(B) ææ¾ç¤ºçå¾åçé¢è²ééä¹ä¾æ¬¡ä¸ºï¼Gï¼Gï¼Gï¼åï¼Bï¼Bï¼Bï¼ã

èå½ä¸ä¸ªééçå¼ç¸åæ¶ï¼åä¸ºç°åº¦å¾ã

æäººå¯è½ä¼é®ï¼ä¸æ¯ Rï¼Gï¼B åï¼ä¸ºä»ä¹ B ééåèæ¾å¨å¾åçç¬¬ä¸ä½ï¼å¦ï¼Bï¼0ï¼0ï¼ï¼

å ä¸º opencv ä¸­ï¼å°±æ¯è°è¿æ¥çï¼å¾åçç¬¬ä¸ééæ¯ Bï¼ç¬¬äºééæ¯ Gï¼æåæ¯ Rã

ä¸é¢å°ä½¿ç¨ merge() å½æ°å°æä¸é¢è²ééï¼å¦ Rï¼ä¸é¶ç©éµåå¹¶ï¼å½¢æï¼Rï¼0ï¼0ï¼ä»èæ¾ç¤ºåªæçº¢è²ééçå¾



### cv.merge() å½æ°çä½¿ç¨

```python
import numpy as np
import cv2     

# è¯»åè¦å¤ççå¾ç
image=cv2.imread(".../default.png")

# åç¦»åºå¾çç Bï¼Rï¼G é¢è²éé
B, G, R = cv2.split(image)    

# åå»ºä¸ image ç¸åå¤§å°çé¶ç©éµ
zeros = np.zeros(image.shape[:2], dtype="uint8")

# æ¾ç¤ºï¼0ï¼0ï¼Rï¼å¾å
cv2.imshow("RED",cv2.merge([zeros, zeros, R]))

# æ¾ç¤ºï¼0ï¼Gï¼0ï¼å¾å
cv2.imshow("GREEN",cv2.merge([zeros, G, zeros]))

# æ¾ç¤º ï¼Bï¼0ï¼0ï¼å¾å
cv2.imshow("BLUE",cv2.merge([B, zeros, zeros]))

cv2.waitKey(0)
```

è¿è¡ç»æä¼åå«æ¾ç¤ºä¸å¼ å¾

æä»¬æåå°è¯æ åç¦»åºæ¥ç Rï¼Gï¼B ééçå¼éæ°åå¹¶å¨ä¸èµ·ï¼çæ¯å¦è½è·å¾åå¾ï¼

```python
import numpy as np
import cv2


# è¯»åè¦å¤ççå¾ç
image=cv2.imread(".../default.png")

# åç¦»åºå¾çç Bï¼Rï¼G é¢è²éé
B, G, R = cv2.split(image)

# åå»ºä¸ image ç¸åå¤§å°çé¶ç©éµ
zeros = np.zeros(image.shape[:2], dtype="uint8")

cv2.imshow("MERGE", cv2.merge([B, G, R]))

cv2.waitKey(0)
```

ç»æè·å¾åå¾



è§é¢éé¢çä»£ç ï¼ä¸æ¯å¾æ

```python
import cv2 as cv
import numpy as np


def bitwise_demo():
    b1 = cv.imread("C:/Users/26368/Desktop/pngtest.png")
    print(b1.shape)
    cv.imshow("input",b1)
    cv.imshow("b1",b1[:,:,2])
    mv=cv.split(b1)#mvä¹å¯ä»¥æ¢æB,G,Rââåå«ä¸ºåç¦»åºæ¥çå¾ççBï¼Rï¼G é¢è²éé
    mv[2][:,:]=255
    result=cv.merge(mv)
    cv.imshow("result",result)
    cv.waitKey(0)
    cv.destroyAllWindows()


if __name__ == "__main__":
    bitwise_demo()
```



### å¾åè²å½©ç©ºé´è½¬æ¢

ï¼æç»¿è²æååºæ¥ï¼

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





### å¾ååç´ å¼ç»è®¡

meanï¼è¾åºåæ°ï¼è®¡ç®åå¼

stddevï¼è¾åºåæ°ï¼è®¡ç®æ åå·®

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





### å¾å½¢å ä½å½¢ç¶ç»å¶

```python
import cv2 as cv
import numpy as np


def demo():
    b1 = cv.imread("C:/Users/26368/Desktop/peoplepng.png")
    #temp=np.copy(b1)
    cv.rectangle(b1,(5,5),(690,650),(0,0,255),4,8,0)
    #(5,5)æ¯å·¦ä¸è§çåæ ï¼ï¼690,650ï¼æ¯å³ä¸è§åæ ï¼ï¼0,0,255ï¼æ¯é¢è²(RGB)ï¼int thickness=4(å¦ææ¯è´æ°å°±å®å¿ï¼å¦ææ¯0çè¯è¿æ¯ä¼æçº¿), int lineType=8, int shift=0
    # thickness:çº¿æ¡çç²ç»ç¨åº¦ãåè´å¼æ¶ï¼å¦ CV_FILLEDï¼å½æ°ç»å¶å¡«åäºè²å½©çç©å½¢ã
    # line_type:çº¿æ¡çç±»åãè§cvLineçæè¿°
    # shift:åæ ç¹çå°æ°ç¹ä½æ°
    cv.circle(b1,(300,300),350,(0,255,255),4,8,0)
    #(300,300)åå¿åæ  350åå¾
    cv.line(b1,(30,30),(300,300),(0,255,255),4,8,0)
    cv.putText(b1,"99%face",(50,50),cv.FONT_HERSHEY_SIMPLEX,1.0,(0,255,255),2,8)
    # å¨å¾åä¸ç»å¶æå­
    # void cv.putText(å¾ç»å¶çå¾å,æå­,ææ¬æ¡å·¦ä¸è§çåæ ,å­ä½(å¦cv::FONT_HERSHEY_PLAIN),å°ºå¯¸(å¼è¶å¤§æå­è¶å¤§),é¢è²ï¼RGBï¼
    # int thicknessçº¿æ¡å®½åº¦,lineType = 8, çº¿åï¼4é»åæ8é»åï¼é»è®¤8é»åï¼,bool bottomLeftOrigin :ä¸ºTrueæ¶å¾åæå­ç¿»è½¬,é»è®¤ä¸º0)

    cv.imshow("input",b1)
    cv.waitKey(0)
    cv.destroyAllWindows()


if __name__ == "__main__":
    demo()

```



### éæºæ°åéæºé¢è²

```python
import cv2 as cv
import numpy as np


def demo():
    b1 = np.zeros((512, 512, 3), dtype=np.uint8)
    while True:
        xx = np.random.randint(0, 512, 2, dtype=np.int)
        # numpy.random.randint(low, high=None, size=None, dtype='l'å¦int64ãint)
        # è¿åä¸ä¸ªéæºæ´åæ°ï¼èå´ä»ä½ï¼åæ¬ï¼å°é«ï¼ä¸åæ¬ï¼ï¼å³[low, high)ã
        # å¦ææ²¡æååæ°highçå¼ï¼åè¿å[0, low)çå¼ã
        # size:è¾åºéæºæ°çå°ºå¯¸ï¼æ¯å¦size = (m * n * k),è¿éè¿åçæ¯äºç»´æ°ç»
        # åè¾åºåè§æ¨¡å³m * n * kä¸ªéæºæ°ãé»è®¤æ¯Noneçï¼ä»ä»è¿åæ»¡è¶³è¦æ±çåä¸éæºæ°ã
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





### å¤è¾¹å½¢å¡«åä¸ç»å¶

```python
import cv2 as cv
import numpy as np


def demo():
    canvas = np.zeros((512, 512, 3), dtype=np.uint8)
    pts = np.array([[100, 100], [350, 100], [450, 280], [
                   320, 450], [80, 400], [30, 300]], dtype=np.int32)

    cv.fillPoly(canvas, [pts], (0, 0, 255), 8, 0)

    # cv.polylines(canvas,[pts],True,(0,0,255),2,8,0)
    # void cv.PolyLine(å¾å, CvPoint ** ptsï¼æçº¿çé¡¶ç¹æéæ°ç»ï¼,int is_closedï¼æåºå¤è¾¹å½¢æ¯å¦å°é­ãå¦æå°é­ï¼å½æ°å°èµ·å§ç¹åç»æç¹è¿çº¿ï¼,
    # é¢è², int thickness = 1, int line_type = 8ï¼çº¿æ®µçç±»åãåè§cvLineï¼, int shift = 0ï¼é¡¶ç¹çå°æ°ç¹ä½æ°ï¼)

    # cv.drawContours(canvas, [pts], -1, (255, 0, 0),4)
    # -1æ¯ int contourIdx, // éè¦ç»å¶çè½®å»çææ° (-1 è¡¨ç¤º "all")
    # 4æ¯å®½åº¦
    cv.imshow("new", canvas)
    cv.waitKey(0)
    cv.destroyAllWindows()


if __name__ == "__main__":
    demo()

```

