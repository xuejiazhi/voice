# voice
# VOSK Kali-CN 语音识别模型
Vosk是基于Kaldi集成的一个轻量级平台服务器，它可以实现和多种服务器端协议集成
国内感觉没法直接在Docker Hub上面下载，特提供了一个下载的Docker镜像包百度网盘的下载

- 通过网盘分享的文件：kali-cn.tar 链接: https://pan.baidu.com/s/18eiBLGBI5ESkYsd02QlDpg 提取码: suum <br/>
~~~C
docker load -i kali-cn.tar
docker run -d -p 2700:2700 alphacep/kaldi-cn:latest
~~~
下载镜像文件到服务器，装好docker,然后把镜像load到本地，再run镜像，就可以将VOSK Kali中文语音识别模型搭建好了，
具体怎么应用看这里
## https://alphacephei.com/vosk/
安装好后测试如下
![8cb271574fff4a8afdcad4ca7d53208](https://github.com/user-attachments/assets/439db00b-ca82-4173-8fb0-8f06acd76c3a)
![4a49df37cc788db27d54be82c097228](https://github.com/user-attachments/assets/f9172186-228f-4b17-a542-716b905c13ee)

# 阿里的FunASR 语音识别模型
FunASR是阿里达摩院提供一个基础的语音识别工具包，提供多种功能，包括语音识别（ASR）、语音端点检测（VAD）、标点恢复（PR）、语言模型（LM）、说话人分离
提供一个Docker 的镜像包百度网盘下载
~~~C
链接:https://pan.baidu.com/s/1PTVgR2WLgsKoXYBrr0ovIw?pwd=sjnc 提取码:sjnc 
复制这段内容后打开百度网盘手机App，操作更方便哦
docker load -i funasr.tar
# 当前文件路径下创建目录 用于挂载模型
mkdir -p ./funasr-runtime-resources/models

# 启动镜像
sudo docker run -p 10095:10095 -it --privileged=true \
-v $PWD/funasr-runtime-resources/models:/workspace/models \
registry.cn-hangzhou.aliyuncs.com/funasr_repo/funasr:funasr-runtime-sdk-cpu-0.4.6

~~~
服务端启动
docker启动之后，进入到docker里边

docker exec -it <imageid> /bin/bash
1
启动funasr-wss-server服务程序（有16K 和 8K模型可选择）：

cd FunASR/runtime
nohup bash run_server.sh \
--download-model-dir /workspace/models \
--vad-dir damo/speech_fsmn_vad_zh-cn-16k-common-onnx \
--model-dir damo/speech_paraformer-large-vad-punc_asr_nat-zh-cn-16k-common-vocab8404-onnx \
--punc-dir damo/punc_ct-transformer_cn-en-common-vocab471067-large-onnx \
--lm-dir damo/speech_ngram_lm_zh-cn-ai-wesp-fst \
--itn-dir thuduj12/fst_itn_zh \
--hotword /workspace/models/hotwords.txt > log.txt 2>&1 &
1
2
3
4
5
6
7
8
9
查看打印日志

tail -f log.txt
————————————————

                            版权声明：本文为博主原创文章，遵循 CC 4.0 BY-SA 版权协议，转载请附上原文出处链接和本声明。
                        
原文链接：https://blog.csdn.net/qq_39035267/article/details/143462888
