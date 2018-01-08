安装ocr库
```
pip install pytesseract
```
安装ocr程序

```
https://www.archlinux.org/packages/community/x86_64/tesseract/download/
```

然后写一个测试 test.py
```
#!/usr/bin/env python3
# -*- coding: utf-8 -*-

import pytesseract
from PIL import Image

# open image
image = Image.open('test.jpg')
code = pytesseract.image_to_string(image, lang='chi_sim')
print(code)
```

运行，发现一个错误：

```
$ python test.py
Traceback (most recent call last):
  File "test.py", line 9, in <module>
    code = pytesseract.image_to_string(image, lang='chi_sim')
  File "/usr/lib/python3.6/site-packages/pytesseract/pytesseract.py", line 125, in image_to_string
    raise TesseractError(status, errors)
pytesseract.pytesseract.TesseractError: (1, 'Error opening data file 
/usr/share/tessdata/chi_sim.traineddata')

```

原来是需要安装中文训练集，下载到/usr/share/tessdata/chi_sim.traineddata即可。
https://github.com/tesseract-ocr/tessdata/blob/master/chi_sim.traineddata


如果没有权限，下载到任意文件夹，然后用sudo cp命令拷贝即可。


然后随便拍一张，但发现效果并不是很好哈～
```
$python test.py
俨伞驴咖叭咖驴呐」鲫
经典旧电国国谱

)′'′\一】 ' 刘 霞 编著

- 幡选卫伽例心电陆 所选心电图改变典型. 病变涵蒜面广, 包韬单病变心电图变化及多
种病变的组台变化。
- 配合分鳙腻 邋慵嘴地癫示心电凰交化及其发生机腩.
妻 嵩

```

如果想要识别更多的文字，可以下载整个训练集：

```
https://github.com/tesseract-ocr/tessdata
```

