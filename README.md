# Brak
> An audio library for training speaker encoders. Currently implemented in Pytorch, Jax support soon.


```
#
```

## Modules

At the moment, Brak only includes a speaker encoder for producing embeddings. The PyTorch implementation is inspired by [Resemblyzer](https://github.com/resemble-ai/Resemblyzer) and [Mozilla TTS](https://github.com/mozilla/TTS/tree/master/speaker_encoder). Both are PyTorch implementations of [GE2E Loss, Generalized End-To-End Loss For Speaker Verification (1710.10467)](https://arxiv.org/pdf/1710.10467.pdf). 

## Pretrained Models:

Model achieves SOTA on the VoxCeleb1 test set at ~1.2% Equal Error Rate (EER) *under 20k steps*. The current model has only been trained on the VoxCeleb1 training set on a single V100 GPU. Model converges at 0.2040 Cross-Entropy Loss and 0.7% EER.

## Speaker Encoder

Embeddings from speaker encoders are a critical component for conditioning decoder synthesizers and output vocoders for speech-to-speech learning. 

Brak differs from current implementations of speaker encoders which use 3-layer vanilla LSTMs with GE2E loss by swapping out the LSTMs for [Li-GRUs (1803.10225)](https://arxiv.org/abs/1803.10225). Additionally, Brak departs from Li-GRUs by using [Mish (1908.08681)](https://arxiv.org/abs/1908.08681) instead of ReLU and [Ranger](https://github.com/lessw2020/Ranger-Deep-Learning-Optimizer)--an optimizer combining [RAdam (1908.03265)](https://arxiv.org/abs/1908.03265), [LookAhead (1907.08610)](https://arxiv.org/abs/1907.08610), and [Gradient Centralization (2004.01461)](https://arxiv.org/abs/2004.01461v2)--instead of Adam.


## Install

`pip install brak`

## How to use

```
1+1
```




    2


