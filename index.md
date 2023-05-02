# SLMGAN

In recent years, large-scale pre-trained speech language models (SLMs) have demonstrated remarkable advancements in various generative speech modeling applications, such as text-to-speech synthesis, voice conversion, and speech enhancement. These applications typically involve mapping text or speech inputs to pre-trained SLM representations, from which target speech is decoded. This paper introduces a new approach, SLMGAN, to leverage SLM representations for discriminative tasks within the generative adversarial network (GAN) framework, specifically for voice conversion. Building upon StarGANv2-VC, we add our novel SLM-based WavLM discriminators on top of the mel-based discriminators along with our newly designed SLM feature matching loss function, resulting in an unsupervised zero-shot voice conversion system that does not require text labels during training. Subjective evaluation results show that SLMGAN outperforms existing state-of-the-art zero-shot voice conversion models in terms of naturalness and achieves comparable similarity, highlighting the potential of SLM-based discriminators for related applications.

---

## Zero-Shot Conversion

All of the following audios are converted from **an unseen speaker** to **another unseen speaker** during training. For a fair comparison to the baseline models, all audios are downsampled to 16k Hz. The input to VC models was trimmed so the output has a different length from the input. 

**All utterances are completely unseen during training, and the results are uncurated (NOT cherry-picked) unless otherwise specified**.

For more audio samples, please go to our survey used for MOS evaluation [here](https://survey.alchemer.com/s3/7323195/VC-wavLM-GT-0424).  You may have to randomly select some answers before proceeding to the next page.

**Sample 1 and 2**

|              | Sample 1 (p234 → p248) | Sample 2 (p261 → p245) |
|:------------:|:-------:|:-------:|
|    **Source**    |    <audio controls="controls">  <source type="audio/wav" src="https://raw.githubusercontent.com/sfmgan/sfmgan.github.io/main/demo/source/11.wav"></source> </audio>   |    <audio controls="controls">  <source type="audio/wav" src="https://raw.githubusercontent.com/sfmgan/sfmgan.github.io/main/demo/source/39.wav"></source> </audio>  |
|    **Target**    |     <audio controls="controls">  <source type="audio/wav" src="https://raw.githubusercontent.com/sfmgan/sfmgan.github.io/main/demo/gt/11.wav"></source> </audio>   |     <audio controls="controls">  <source type="audio/wav" src="https://raw.githubusercontent.com/sfmgan/sfmgan.github.io/main/demo/gt/39.wav"></source> </audio> |
|    **AGAIN-VC**   |     <audio controls="controls">  <source type="audio/wav" src="https://raw.githubusercontent.com/sfmgan/sfmgan.github.io/main/demo/againvc/11.wav"></source> </audio>    |     <audio controls="controls">  <source type="audio/wav" src="https://raw.githubusercontent.com/sfmgan/sfmgan.github.io/main/demo/againvc/39.wav"></source> </audio>     |
|    **VQMIVC-VC**   |     <audio controls="controls">  <source type="audio/wav" src="https://raw.githubusercontent.com/sfmgan/sfmgan.github.io/main/demo/vqmivc/11.wav"></source> </audio>    |     <audio controls="controls">  <source type="audio/wav" src="https://raw.githubusercontent.com/sfmgan/sfmgan.github.io/main/demo/vqmivc/39.wav"></source> </audio>     |
| **YourTTS** |    <audio controls="controls">  <source type="audio/wav" src="https://raw.githubusercontent.com/sfmgan/sfmgan.github.io/main/demo/yourtts/11.wav"></source> </audio>     |    <audio controls="controls">  <source type="audio/wav" src="https://raw.githubusercontent.com/sfmgan/sfmgan.github.io/main/demo/yourtts/39.wav"></source> </audio>      |
| **StyleTTS-VC** |    <audio controls="controls">  <source type="audio/wav" src="https://raw.githubusercontent.com/sfmgan/sfmgan.github.io/main/demo/stylettsvc/11.wav"></source> </audio>     |    <audio controls="controls">  <source type="audio/wav" src="https://raw.githubusercontent.com/sfmgan/sfmgan.github.io/main/demo/stylettsvc/39.wav"></source> </audio>      |
| **SLMGAN (Proposed)** |    <audio controls="controls">  <source type="audio/wav" src="https://raw.githubusercontent.com/sfmgan/sfmgan.github.io/main/demo/slmgan/11.wav"></source> </audio>     |    <audio controls="controls">  <source type="audio/wav" src="https://raw.githubusercontent.com/sfmgan/sfmgan.github.io/main/demo/slmgan/39.wav"></source> </audio>      |

**Sample 3 and 4**

|              | Sample 3 (p347 → p326) | Sample 4 (p261 → p234) |
|:------------:|:-------:|:-------:|
|    **Source**    |    <audio controls="controls">  <source type="audio/wav" src="https://raw.githubusercontent.com/sfmgan/sfmgan.github.io/main/demo/source/65.wav"></source> </audio>   |    <audio controls="controls">  <source type="audio/wav" src="https://raw.githubusercontent.com/sfmgan/sfmgan.github.io/main/demo/source/68.wav"></source> </audio>  |
|    **Target**    |     <audio controls="controls">  <source type="audio/wav" src="https://raw.githubusercontent.com/sfmgan/sfmgan.github.io/main/demo/gt/65.wav"></source> </audio>   |     <audio controls="controls">  <source type="audio/wav" src="https://raw.githubusercontent.com/sfmgan/sfmgan.github.io/main/demo/gt/68.wav"></source> </audio> |
|    **AGAIN-VC**   |     <audio controls="controls">  <source type="audio/wav" src="https://raw.githubusercontent.com/sfmgan/sfmgan.github.io/main/demo/againvc/65.wav"></source> </audio>    |     <audio controls="controls">  <source type="audio/wav" src="https://raw.githubusercontent.com/sfmgan/sfmgan.github.io/main/demo/againvc/68.wav"></source> </audio>     |
|    **VQMIVC-VC**   |     <audio controls="controls">  <source type="audio/wav" src="https://raw.githubusercontent.com/sfmgan/sfmgan.github.io/main/demo/vqmivc/65.wav"></source> </audio>    |     <audio controls="controls">  <source type="audio/wav" src="https://raw.githubusercontent.com/sfmgan/sfmgan.github.io/main/demo/vqmivc/68.wav"></source> </audio>     |
| **YourTTS** |    <audio controls="controls">  <source type="audio/wav" src="https://raw.githubusercontent.com/sfmgan/sfmgan.github.io/main/demo/yourtts/65.wav"></source> </audio>     |    <audio controls="controls">  <source type="audio/wav" src="https://raw.githubusercontent.com/sfmgan/sfmgan.github.io/main/demo/yourtts/68.wav"></source> </audio>      |
| **StyleTTS-VC** |    <audio controls="controls">  <source type="audio/wav" src="https://raw.githubusercontent.com/sfmgan/sfmgan.github.io/main/demo/stylettsvc/65.wav"></source> </audio>     |    <audio controls="controls">  <source type="audio/wav" src="https://raw.githubusercontent.com/sfmgan/sfmgan.github.io/main/demo/stylettsvc/68.wav"></source> </audio>      |
| **SLMGAN (Proposed)** |    <audio controls="controls">  <source type="audio/wav" src="https://raw.githubusercontent.com/sfmgan/sfmgan.github.io/main/demo/slmgan/65.wav"></source> </audio>     |    <audio controls="controls">  <source type="audio/wav" src="https://raw.githubusercontent.com/sfmgan/sfmgan.github.io/main/demo/slmgan/68.wav"></source> </audio>      |

**Sample 5 and 6**

|              | Sample 5 (p248 → p261) | Sample 6 (p234 → p245) |
|:------------:|:-------:|:-------:|
|    **Source**    |    <audio controls="controls">  <source type="audio/wav" src="https://raw.githubusercontent.com/sfmgan/sfmgan.github.io/main/demo/source/33.wav"></source> </audio>   |    <audio controls="controls">  <source type="audio/wav" src="https://raw.githubusercontent.com/sfmgan/sfmgan.github.io/main/demo/source/0.wav"></source> </audio>  |
|    **Target**    |     <audio controls="controls">  <source type="audio/wav" src="https://raw.githubusercontent.com/sfmgan/sfmgan.github.io/main/demo/gt/33.wav"></source> </audio>   |     <audio controls="controls">  <source type="audio/wav" src="https://raw.githubusercontent.com/sfmgan/sfmgan.github.io/main/demo/gt/0.wav"></source> </audio> |
|    **AGAIN-VC**   |     <audio controls="controls">  <source type="audio/wav" src="https://raw.githubusercontent.com/sfmgan/sfmgan.github.io/main/demo/againvc/33.wav"></source> </audio>    |     <audio controls="controls">  <source type="audio/wav" src="https://raw.githubusercontent.com/sfmgan/sfmgan.github.io/main/demo/againvc/0.wav"></source> </audio>     |
|    **VQMIVC-VC**   |     <audio controls="controls">  <source type="audio/wav" src="https://raw.githubusercontent.com/sfmgan/sfmgan.github.io/main/demo/vqmivc/33.wav"></source> </audio>    |     <audio controls="controls">  <source type="audio/wav" src="https://raw.githubusercontent.com/sfmgan/sfmgan.github.io/main/demo/vqmivc/0.wav"></source> </audio>     |
| **YourTTS** |    <audio controls="controls">  <source type="audio/wav" src="https://raw.githubusercontent.com/sfmgan/sfmgan.github.io/main/demo/yourtts/33.wav"></source> </audio>     |    <audio controls="controls">  <source type="audio/wav" src="https://raw.githubusercontent.com/sfmgan/sfmgan.github.io/main/demo/yourtts/0.wav"></source> </audio>      |
| **StyleTTS-VC** |    <audio controls="controls">  <source type="audio/wav" src="https://raw.githubusercontent.com/sfmgan/sfmgan.github.io/main/demo/stylettsvc/33.wav"></source> </audio>     |    <audio controls="controls">  <source type="audio/wav" src="https://raw.githubusercontent.com/sfmgan/sfmgan.github.io/main/demo/stylettsvc/0.wav"></source> </audio>      |
| **SLMGAN (Proposed)** |    <audio controls="controls">  <source type="audio/wav" src="https://raw.githubusercontent.com/sfmgan/sfmgan.github.io/main/demo/slmgan/33.wav"></source> </audio>     |    <audio controls="controls">  <source type="audio/wav" src="https://raw.githubusercontent.com/sfmgan/sfmgan.github.io/main/demo/slmgan/0.wav"></source> </audio>      |

---

## Ablation Study

We present four samples of ablation study for conditions described in Table 3 in our paper on VCTK dataset. 

**Sample 1 and 2**

|              | Sample 1 | Sample 2 |
|:------------:|:-------:|:-------:|
|    **Source**    |    <audio controls="controls">  <source type="audio/wav" src="https://raw.githubusercontent.com/sfmgan/sfmgan.github.io/main/ablation/source/2.wav"></source> </audio>   |    <audio controls="controls">  <source type="audio/wav" src="https://raw.githubusercontent.com/sfmgan/sfmgan.github.io/main/ablation/source/15.wav"></source> </audio>  |
|    **Target**    |     <audio controls="controls">  <source type="audio/wav" src="https://raw.githubusercontent.com/sfmgan/sfmgan.github.io/main/ablation/gt/2.wav"></source> </audio>   |     <audio controls="controls">  <source type="audio/wav" src="https://raw.githubusercontent.com/sfmgan/sfmgan.github.io/main/ablation/gt/15.wav"></source> </audio> |
|    **Baseline**   |     <audio controls="controls">  <source type="audio/wav" src="https://raw.githubusercontent.com/sfmgan/sfmgan.github.io/main/ablation/baseline/2.wav"></source> </audio>    |     <audio controls="controls">  <source type="audio/wav" src="https://raw.githubusercontent.com/sfmgan/sfmgan.github.io/main/ablation/baseline/15.wav"></source> </audio>     |
|    **No SFM Discriminators**   |     <audio controls="controls">  <source type="audio/wav" src="https://raw.githubusercontent.com/sfmgan/sfmgan.github.io/main/ablation/nosfm/2.wav"></source> </audio>    |     <audio controls="controls">  <source type="audio/wav" src="https://raw.githubusercontent.com/sfmgan/sfmgan.github.io/main/ablation/nosfm/15.wav"></source> </audio>     |
|    **No SFM Loss**   |     <audio controls="controls">  <source type="audio/wav" src="https://raw.githubusercontent.com/sfmgan/sfmgan.github.io/main/ablation/nofm/2.wav"></source> </audio>    |     <audio controls="controls">  <source type="audio/wav" src="https://raw.githubusercontent.com/sfmgan/sfmgan.github.io/main/ablation/nofm/15.wav"></source> </audio>     |

**Sample 3 and 4**

|              | Sample 3 | Sample 4 |
|:------------:|:-------:|:-------:|
|    **Source**    |    <audio controls="controls">  <source type="audio/wav" src="https://raw.githubusercontent.com/sfmgan/sfmgan.github.io/main/ablation/source/40.wav"></source> </audio>   |    <audio controls="controls">  <source type="audio/wav" src="https://raw.githubusercontent.com/sfmgan/sfmgan.github.io/main/ablation/source/25.wav"></source> </audio>  |
|    **Target**    |     <audio controls="controls">  <source type="audio/wav" src="https://raw.githubusercontent.com/sfmgan/sfmgan.github.io/main/ablation/gt/40.wav"></source> </audio>   |     <audio controls="controls">  <source type="audio/wav" src="https://raw.githubusercontent.com/sfmgan/sfmgan.github.io/main/ablation/gt/25.wav"></source> </audio> |
|    **Baseline**   |     <audio controls="controls">  <source type="audio/wav" src="https://raw.githubusercontent.com/sfmgan/sfmgan.github.io/main/ablation/baseline/40.wav"></source> </audio>    |     <audio controls="controls">  <source type="audio/wav" src="https://raw.githubusercontent.com/sfmgan/sfmgan.github.io/main/ablation/baseline/25.wav"></source> </audio>     |
|    **No SFM Discriminators**   |     <audio controls="controls">  <source type="audio/wav" src="https://raw.githubusercontent.com/sfmgan/sfmgan.github.io/main/ablation/nosfm/40.wav"></source> </audio>    |     <audio controls="controls">  <source type="audio/wav" src="https://raw.githubusercontent.com/sfmgan/sfmgan.github.io/main/ablation/nosfm/25.wav"></source> </audio>     |
|    **No SFM Loss**   |     <audio controls="controls">  <source type="audio/wav" src="https://raw.githubusercontent.com/sfmgan/sfmgan.github.io/main/ablation/nofm/40.wav"></source> </audio>    |     <audio controls="controls">  <source type="audio/wav" src="https://raw.githubusercontent.com/sfmgan/sfmgan.github.io/main/ablation/nofm/25.wav"></source> </audio>     |

