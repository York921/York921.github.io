---
layout: post
title:  "Python OCR之Pytesser安装"
date:   2014-8-14 00:25:00
categories: Python
---

最近研究OCR，在python中使用最广泛的库是Pytesser，包装了谷歌的Tesseract，后者号称是最准确的开源OCR引擎。

####安装

#####Python Imaging Library (PIL)

Python图像处理最常用的库，功能也十分强大。

```bash
curl -OL http://effbot.org/downloads/Imaging-1.1.7.tar.gz
tar xzvf Imaging-1.1.7.tar.gz && cd Imaging-1.1.7
python setup.py install
```

如果提示`fatal error: 'freetype/fterrors.h' file not found`则需要下载编译`freetype2`并把`setup.py`的`FREETYPE_ROOT`改成实际的头文件路径。

#####Tesseract
首先下载安装Tesseract所依赖的开源图像处理库[`leptonica`](http://cjj.kr.distfiles.macports.org/leptonica/leptonica-1.71.tar.gz)

```bash
./configure
make
sudo make install
```

然后下载[`Tesseract`](http://cjj.kr.distfiles.macports.org/tesseract/tesseract-3.02.02.tar.gz)
进入目录执行`./autogen.sh`后重复上面的三步便安装完毕。

识别图片时需要相应语言的数据集，附带的测试图片需要[`英文数据集`](http://cjj.kr.distfiles.macports.org/tesseract/tesseract-ocr-3.01.eng.tar.gz)。

下载完成后需要把`tessdata`中文件解压至默认数据集路径`/usr/local/share/tessdata`中即可。

在实际使用时也可以修改环境变量来指定数据集路径，具体参考文档。

#####Pytesser
最后安装Pytesser，之前解决了所有依赖项，接下来十分顺利了。

```bash
git clone https://github.com/madmaze/pytesseract.git --single-branch
cd pytesseract
sudo python setup.py install
```

验证一下：

```Python3
import Image
import pytesseract
print pytesseract.image_to_string(Image.open('test.png'))
```

原图：
![ocr-test](/assets/images/ocr-test.png)

识别结果：
![ocr-result](/assets/images/ocr-result.png)




