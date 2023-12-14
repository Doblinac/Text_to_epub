
这是一款用安卓手机把txt文件转化为epub电子书的python程序，安卓系统需要安装termux，termux要安装python,具体termux使用方法请网上查阅。

1.把下载的Text_to_epub.zip解压到任意文件夹。

2.把要转化的txt文件改名为book.txt并复制到Converter文件夹。

3.准备一张封面图片，改名为00000.jpg，放入Converter文件夹。

4.整理电子书目录，每行一个目录（不用标点）复制到NCX.txt文件。

5.启动termux软件，进入你解压的文件夹（最好是预先设置好超链接），运行： python complete.py

6.到解压的文件夹找到book.epub，这就是转化好的电子书。

附注：所用txt文档最好是用OCR软件转自PDF的电子书。

   制作：doblinac
