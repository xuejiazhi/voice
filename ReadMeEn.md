# voice
# VOSK Kali-CN Speech recognition model
Vosk is a lightweight platform server based on Kaldi integration, which can integrate with multiple server-side protocols
I feel that it is not possible to download directly on Docker Hub in China, so I have provided a downloadable Docker image package for Baidu Netdisk

- Files shared through online storage：kali-cn.tar LINK: https://pan.baidu.com/s/18eiBLGBI5ESkYsd02QlDpg Extracted code: suum <br/>
~~~C
docker load -i kali-cn.tar
docker run -d -p 2700:2700 alphacep/kaldi-cn:latest
~~~
Download the image file to the server, install Docker, then load the image locally, and run the image to build the VOSK Kali Chinese speech recognition model,
See here for specific applications
## https://alphacephei.com/vosk/
After installation, the test is as follows
![8cb271574fff4a8afdcad4ca7d53208](https://github.com/user-attachments/assets/439db00b-ca82-4173-8fb0-8f06acd76c3a)
![4a49df37cc788db27d54be82c097228](https://github.com/user-attachments/assets/f9172186-228f-4b17-a542-716b905c13ee)

# Alibaba's FunASR speech recognition model
FunASR is a basic speech recognition toolkit provided by Alibaba Institute, offering multiple functions including speech recognition (ASR), speech endpoint detection (VAD), punctuation recovery (PR), language modeling (LM), and speaker separation
Provide a Docker image package for Baidu Netdisk download
- LINK:https://pan.baidu.com/s/1PTVgR2WLgsKoXYBrr0ovIw?pwd=sjnc Extracted code:sjnc 
- After copying this content, open the Baidu Netdisk mobile app for more convenient operation
~~~C
docker load -i funasr.tar
~~~
# Create a directory under the current file path to mount the model
~~~C
mkdir -p ./funasr-runtime-resources/models
~~~
# Start image
~~~C
sudo docker run -p 10095:10095 -it --privileged=true \
-v $PWD/funasr-runtime-resources/models:/workspace/models \
registry.cn-hangzhou.aliyuncs.com/funasr_repo/funasr:funasr-runtime-sdk-cpu-0.4.6
~~~
After the server starts and Docker starts, it enters Docker
~~~C
docker exec -it <imageid> /bin/bash
~~~
Start the funasr wss server service program (with 16K and 8K models to choose from):
~~~C
cd FunASR/runtime
nohup bash run_server.sh \
--download-model-dir /workspace/models \
--vad-dir damo/speech_fsmn_vad_zh-cn-16k-common-onnx \
--model-dir damo/speech_paraformer-large-vad-punc_asr_nat-zh-cn-16k-common-vocab8404-onnx \
--punc-dir damo/punc_ct-transformer_cn-en-common-vocab471067-large-onnx \
--lm-dir damo/speech_ngram_lm_zh-cn-ai-wesp-fst \
--itn-dir thuduj12/fst_itn_zh \
--hotword /workspace/models/hotwords.txt > log.txt 2>&1 &
~~~
#View print logs
~~~C
tail -f log.txt
~~~
If you want to turn off SSL, add parameters：--certfile 0
If you want to deploy an 8k model, please use the following command to start the service：
~~~C
cd FunASR/runtime
nohup bash run_server.sh \
--download-model-dir /workspace/models \
--vad-dir damo/speech_fsmn_vad_zh-cn-8k-common-onnx \
--model-dir damo/speech_paraformer_asr_nat-zh-cn-8k-common-vocab8358-tensorflow1-onnx \
--punc-dir damo/punc_ct-transformer_cn-en-common-vocab471067-large-onnx \
--lm-dir damo/speech_ngram_lm_zh-cn-ai-wesp-fst-token8358 \
--itn-dir thuduj12/fst_itn_zh \
--hotword /workspace/models/hotwords.txt > log.txt 2>&1 &
~~~
Use client testing
Officially provided：html、java、python、cpp
Download the HTML page from the Docker image to the host machine, and then download it to the local machine
~~~C
docker cp  <Container ID or Name>:/workspace/FunASR/runtime/html5 /funasr-runtime-resources
~~~
Open html/static/index.html in the browser, and the following page will appear, supporting microphone input and file upload for direct experience.
![image](https://github.com/user-attachments/assets/21b57ee6-bcd0-42fa-8093-c43923a62a69)

# WAV data for speech recognition testing
Here is another WAV dataset for speech recognition testing (250 in Chinese and 150 in English)
- LINK:https://pan.baidu.com/s/1VZsJ8ooU9W9m4QNW4NLJ2g?pwd=rih9 Extracted code:rih9 
After copying this content, open the Baidu Netdisk mobile app for more convenient operation
![image](https://github.com/user-attachments/assets/ff53c6ef-a5d6-45fc-a16b-03ffbae1f5e1)
![image](https://github.com/user-attachments/assets/f71ba235-2ae5-457f-b7a3-1517e1bdb8d9)


