# Singing Style Transfer

My contribution on Team Project on Eliceio team4: vocal-style-transfer (https://github.com/eliceio/vocal-style-transfer)

I was in charge of transfering singing style by using separated vocal data(separated by pretrained Deep U net[2]) not by clean speech data. And I adapted BE-GAN[4] training skill to Cycle-GAN-VC[3] refer to Singing Style Transfer C-BEGAN [1].

## 1. Abstract

Whole architecture for changing singing style transfer is shown below [1]

<p align="left">
    <img src = "./image/Main_Architecture.JPG" width="60%">
</p>

## 2. Preprocess


First download songs from "Youtube" by using pytube library.(This might be illegal)

For the vocal data I downloaded Park Hyo Shin and BolBBalGan Sachungi's songs. (about 15 songs each)

For the separation of Singing Voice & Accompaniment I used pretrained deep U-net model. [2]

Finally I removed silence for the bigger receptive field on voices.

Datas were downsampled to 16 kHz. For the separation normalized magnitude spectrogram were used and for the transfer  24 Mel-cepstral coefficients (MCEPs) were used.[2][3]



## 3. Cycle Consistency - Boundary Equilibrium GAN

Since the singers we want to change don't sing same songs(Unpaired Data) I used Cycle-Gan for the transferring singing style.[1] Main model of Cycle-Gan is from "Cycle Gan Voice Converter".[3]

Due to the differeces between voice converting and transferring singing style I expanded frames to 512. Which frames were 128 (about 0.5sec) from "Cycle Gan Voice Converter".

Also I modified adversarial Loss functions, Discriminator and added hyper-parameters to adjust BEGAN to cycle-gan for the stablizing training process.[1][4]


### 3-1.  Generator & Discriminator Architectures



<p>
    <img src = "./image/GD_network.png" width="90%">
</p>




###  3-2.  Loss Function

<p>
    <img align="left" src = "./image/loss_function_1.png" width="100%" height="45">
</p>


where

<p>
    <img align="left" src = "./image/loss_function_2.png" width="60%">
</p>

<br><br><br><br><br><br><br>

## 4. Future Works

More powerful separation for vocal separation.

Embed more information such as lyrics and adjust Tacotron. ex) Tacotron GAN "https://github.com/tmulc18/S2SCycleGAN"



## 5. References

[1] Cheng-Wei Wu, Jen-Yu Liu, Yi-Hsuan Yang, Jyh-Shing R. Jang. Singing Style Transfer Using Cycle-Consistent Boundary Equilibrium Generative Adversarial Networks. 2018 <br> paper: https://arxiv.org/abs/1807.02254

[2] Andreas Jansson, Eric Humphrey, Nicola Montecchio, Rachel Bittner, Aparna Kumar, Tillman Weyde. SINGING VOICE SEPARATION WITH DEEP U-NET CONVOLUTIONAL NETWORKS. 2017. <br> paper: https://ismir2017.smcnus.org/wp-content/uploads/2017/10/171_Paper.pdf <br> code & pretrained model from: https://github.com/Xiao-Ming/UNet-VocalSeparation-Chainer
    
[3] Takuhiro Kaneko, Hirokazu Kameoka. Parallel-Data-Free Voice Conversion Using Cycle-Consistent Adversarial Networks. 2017.<br> paper:https://arxiv.org/abs/1711.11293<br>
code: https://github.com/leimao/Voice_Converter_CycleGAN

[4] David Berthelot, Thomas Schumm, Luke Metz. BEGAN: Boundary Equilibrium Generative Adversarial Networks. 2017.<br> paper:https://arxiv.org/pdf/1703.10717.pdf
<br>code: https://github.com/carpedm20/BEGAN-tensorflow
