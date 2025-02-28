# voice
语音识别模型
Vosk是基于Kaldi集成的一个轻量级平台服务器，它可以实现和多种服务器端协议集成
国内感觉没法直接在Docker Hub上面下载，特提供了一个下载的Docker镜像包百度网盘的下载
~~~C
通过网盘分享的文件：kali-cn.tar
链接: https://pan.baidu.com/s/18eiBLGBI5ESkYsd02QlDpg 提取码: suum
docker load -i kali-cn.tar
docker run -d -p 2700:2700 alphacep/kaldi-cn:latest
~~~
下载镜像文件到服务器，装好docker,然后把镜像load到本地，再run镜像，就可以将VOSK Kali中文语音识别模型搭建好了，
具体怎么应用看这里
## https://alphacephei.com/vosk/
安装好后测试如下
![8cb271574fff4a8afdcad4ca7d53208](https://github.com/user-attachments/assets/439db00b-ca82-4173-8fb0-8f06acd76c3a)
![4a49df37cc788db27d54be82c097228](https://github.com/user-attachments/assets/f9172186-228f-4b17-a542-716b905c13ee)
