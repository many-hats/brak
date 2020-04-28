# Brak
> An in-progress audio library for training speaker encoders. Proof of concept in Pytorch, Jax support soon.


## Modules

At the moment, Brak only includes a speaker encoder for producing embeddings. The PyTorch implementation is a fork of [Resemblyzer](https://github.com/resemble-ai/Resemblyzer) and [Real Time Voice Cloning](https://github.com/CorentinJ/Real-Time-Voice-Cloning). Both are PyTorch implementations of [GE2E Loss, Generalized End-To-End Loss For Speaker Verification (1710.10467)](https://arxiv.org/pdf/1710.10467.pdf) and [Transfer Learning from Speaker Verification to
Multispeaker Text-To-Speech Synthesis](https://arxiv.org/abs/1806.04558) respectively.

## Pretrained Models:

Model achieves SOTA on the VoxCeleb1 test set at ~1.2% Equal Error Rate (EER) *under 20k steps*. The current model has only been trained on the VoxCeleb1 training set on a single V100 GPU. Model converges at 0.2040 Cross-Entropy Loss and 0.7% EER.

## Speaker Encoder

Embeddings from speaker encoders are a critical component for conditioning decoder synthesizers and output vocoders for speech-to-speech learning. 

Brak differs from current implementations of speaker encoders which use 3-layer vanilla LSTMs with GE2E loss by swapping out the LSTMs for [Li-GRUs (1803.10225)](https://arxiv.org/abs/1803.10225). Additionally, Brak departs from Li-GRUs by using [Mish (1908.08681)](https://arxiv.org/abs/1908.08681) instead of ReLU and [Ranger](https://github.com/lessw2020/Ranger-Deep-Learning-Optimizer)--an optimizer combining [RAdam (1908.03265)](https://arxiv.org/abs/1908.03265), [LookAhead (1907.08610)](https://arxiv.org/abs/1907.08610), and [Gradient Centralization (2004.01461)](https://arxiv.org/abs/2004.01461v2)--instead of Adam.


## Model

Li-GRUs were first introduced in [Light Gated Recurrent Units for Speaker Recognition (1803.10225)](https://arxiv.org/abs/1803.10225). The core ideas behind Li-GRUs are that removing the reset gate from GRUs would be helpful as the past state is usually always relevant in the context of speech and coupled ReLU and BatchNorm instead of *tanh*. [PyTorch-Kaldi](https://github.com/mravanelli/pytorch-kaldi) found Li-GRU to be the best performing model on TIMIT, using a bidirectional 5-layer stack of Li-GRUs with `hidden_dim` of 550 and dropout of 0.2 between layers. 

Brak extends this idea to speaker encoding, but replaces the ReLU with Mish. Brak uses a 3-layer stack of Li-GRU's with `hidden_dim` of 256 and dropout of 0.2 between layers. The initial curiosity for the use of Mish arose from its and its predecessor's ([Swish (1710.05941)](https://arxiv.org/abs/1710.05941)) similarity to an inverted low pass filter with resonance. 



**Swish**

<img src="../brak/imgs/swish.png" width="300" height="300">


**Low Pass Filter**

<img src="../brak/imgs/low pass filter with resonance.gif" width="300" height="300">

**Mish**

**Low Pass Filter**

<img src="../brak/imgs/Mish3.png" width="300" height="300">

# Install

```
!git clone https://github.com/many-hats/brak.git
!cd brak 
!git clone https://github.com/many-hats/rtvc
```
