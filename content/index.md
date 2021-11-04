---
date: 2021-11-01T00:00:00+00:00
type: "index"
---

# An investigation of streaming non-autoregressive sequence-to-sequence voice conversion

- Tomoki Hayashi (TARVO Inc. / Nagoya University)
- Kazuhiro Kobayashi (TARVO Inc. / Nagoya University)
- Tomoki Toda (Nagoya University)

## Abstract

Recent advances in sequence-to-sequence (S2S) models have improved the quality of voice conversion (VC), but it requires an entire sequence to perform inference, which prevents using it in real-time applications. To address this issue, this paper extends the non-autoregressive (NAR) S2S-VC model to enable us to perform streaming VC. We introduce streamable architecture such as a causal convolution and a self-attention with causal masking for the FastSpeech2-based NAR-S2S-VC model. This streamable architecture also tries to convert durations, which are kept as is in conventional real-time VC methods. To further improve the performance of the streaming VC model, we utilize an instant knowledge distillation with a dual-mode architecture, which performs non-causal and causal inference by sharing the network parameters. Through the experimental evaluation with Japanese parallel corpus, we investigate the impact on performance caused by the streamable architecture. The experimental results reveal that the use of future context frames increases latency, but it improves the conversion quality, and that difference in the speaking rate affects the performance of streaming inference.

## Audio samples (Japanese)

- **Source**: Source speech (24,000 Hz).
- **Target**: Target speech (24,000 Hz).
- **Non-causal**: Converted speech by non-causal Conformer FastSpeech2 (CFS2) + non-causal parallel wavegan (PWG)
- **Causal (k=0)**: Converted speech by causal CFS2 + causal PWG
- **Causal (k=2)**: Converted speech by causal CFS2 with 2 future frames + causal PWG
- **Causal (k=2) + Knowledge dist.**: Causal (k=2) + Instant Knowledge distillation

### Male to female conversion

#### たとえば、プログラムを書く仕事は、機械なしでも、やろうと思えばできる。

|     |     |
| --- | --- |
| **Source** | **Target** |
|<audio controls="" ><source src="wav/ashela_gt/ETRAB00976.wav"/></audio>|<audio controls="" ><source src="wav/hazumi_gt/ETRAB00976.wav"/></audio>|
| **Non-causal** | **Causal (k=0)** |
|<audio controls="" ><source src="wav/hazumi_noncausal_pwg/ETRAB00976.wav"/></audio>|<audio controls="" ><source src="wav/hazumi_causal_cpwg_hfd/ETRAB00976.wav"/></audio>|
| **Causal (k=2)** | **Causal (k=2) + Knowledge dist.** |
|<audio controls="" ><source src="wav/hazumi_causal_future_cpwg_hfd/ETRAB00976.wav"/></audio>|<audio controls="" ><source src="wav/hazumi_switch_causal_future_cpwg_hfd/ETRAB00976.wav"/></audio>|

#### そのうちに、日が暮れて、寒い風が、ヒューヒュー、吹きはじめました。

|     |     |
| --- | --- |
| **Source** | **Target** |
|<audio controls="" ><source src="wav/ashela_gt/ETRAB00982.wav"/></audio>|<audio controls="" ><source src="wav/hazumi_gt/ETRAB00982.wav"/></audio>|
| **Non-causal** | **Causal (k=0)** |
|<audio controls="" ><source src="wav/hazumi_noncausal_pwg/ETRAB00982.wav"/></audio>|<audio controls="" ><source src="wav/hazumi_causal_cpwg_hfd/ETRAB00982.wav"/></audio>|
| **Causal (k=2)** | **Causal (k=2) + Knowledge dist.** |
|<audio controls="" ><source src="wav/hazumi_causal_future_cpwg_hfd/ETRAB00982.wav"/></audio>|<audio controls="" ><source src="wav/hazumi_switch_causal_future_cpwg_hfd/ETRAB00982.wav"/></audio>|

#### 小柄な男は、部屋の中を、しげしげと、覗き込みながら言った。

|     |     |
| --- | --- |
| **Source** | **Target** |
|<audio controls="" ><source src="wav/ashela_gt/ETRAB00990.wav"/></audio>|<audio controls="" ><source src="wav/hazumi_gt/ETRAB00990.wav"/></audio>|
| **Non-causal** | **Causal (k=0)** |
|<audio controls="" ><source src="wav/hazumi_noncausal_pwg/ETRAB00990.wav"/></audio>|<audio controls="" ><source src="wav/hazumi_causal_cpwg_hfd/ETRAB00990.wav"/></audio>|
| **Causal (k=2)** | **Causal (k=2) + Knowledge dist.** |
|<audio controls="" ><source src="wav/hazumi_causal_future_cpwg_hfd/ETRAB00990.wav"/></audio>|<audio controls="" ><source src="wav/hazumi_switch_causal_future_cpwg_hfd/ETRAB00990.wav"/></audio>|

### Female to male conversion

#### たとえば、プログラムを書く仕事は、機械なしでも、やろうと思えばできる。

|     |     |
| --- | --- |
| **Source** | **Target** |
|<audio controls="" ><source src="wav/hazumi_gt/ETRAB00976.wav"/></audio>|<audio controls="" ><source src="wav/ashela_gt/ETRAB00976.wav"/></audio>|
| **Non-causal** | **Causal (k=0)** |
|<audio controls="" ><source src="wav/ashela_noncausal_pwg/ETRAB00976.wav"/></audio>|<audio controls="" ><source src="wav/ashela_causal_cpwg_hfd/ETRAB00976.wav"/></audio>|
| **Causal (k=2)** | **Causal (k=2) + Knowledge dist.** |
|<audio controls="" ><source src="wav/ashela_causal_future_cpwg_hfd/ETRAB00976.wav"/></audio>|<audio controls="" ><source src="wav/ashela_switch_causal_future_cpwg_hfd/ETRAB00976.wav"/></audio>|

#### そのうちに、日が暮れて、寒い風が、ヒューヒュー、吹きはじめました。

|     |     |
| --- | --- |
| **Source** | **Target** |
|<audio controls="" ><source src="wav/hazumi_gt/ETRAB00982.wav"/></audio>|<audio controls="" ><source src="wav/ashela_gt/ETRAB00982.wav"/></audio>|
| **Non-causal** | **Causal (k=0)** |
|<audio controls="" ><source src="wav/ashela_noncausal_pwg/ETRAB00982.wav"/></audio>|<audio controls="" ><source src="wav/ashela_causal_cpwg_hfd/ETRAB00982.wav"/></audio>|
| **Causal (k=2)** | **Causal (k=2) + Knowledge dist.** |
|<audio controls="" ><source src="wav/ashela_causal_future_cpwg_hfd/ETRAB00982.wav"/></audio>|<audio controls="" ><source src="wav/ashela_switch_causal_future_cpwg_hfd/ETRAB00982.wav"/></audio>|


#### 小柄な男は、部屋の中を、しげしげと、覗き込みながら言った。

|     |     |
| --- | --- |
| **Source** | **Target** |
|<audio controls="" ><source src="wav/hazumi_gt/ETRAB00990.wav"/></audio>|<audio controls="" ><source src="wav/ashela_gt/ETRAB00990.wav"/></audio>|
| **Non-causal** | **Causal (k=0)** |
|<audio controls="" ><source src="wav/ashela_noncausal_pwg/ETRAB00990.wav"/></audio>|<audio controls="" ><source src="wav/ashela_causal_cpwg_hfd/ETRAB00990.wav"/></audio>|
| **Causal (k=2)** | **Causal (k=2) + Knowledge dist.** |
|<audio controls="" ><source src="wav/ashela_causal_future_cpwg_hfd/ETRAB00990.wav"/></audio>|<audio controls="" ><source src="wav/ashela_switch_causal_future_cpwg_hfd/ETRAB00990.wav"/></audio>|

### Controllability analysis

![](figs/example.png)

|     |
| --- |
| **Source** |
|<audio controls="" ><source src="wav/example/src.wav"/></audio>|
| **Target** |
|<audio controls="" ><source src="wav/example/tgt.wav"/></audio>|
| **Conversion** |
|<audio controls="" ><source src="wav/example/conv.wav"/></audio>|
| **Conversion with fixed duration** |
|<audio controls="" ><source src="wav/example/src_dur_fixed_conv.wav"/></audio>|
| **Conversion with fixed pitch, energy, and duration** |
|<audio controls="" ><source src="wav/example/src_all_fixed_conv.wav"/></audio>|

## Author

Tomoki Hayashi ([@kan-bayashi](https://github.com/kan-bayashi))  
e-mail: hayashi.tomoki@g.sp.m.is.nagoya-u.ac.jp
