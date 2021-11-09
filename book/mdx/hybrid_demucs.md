(hybrid_demucs)=

# Hybrid Demucs

Demucs is based on U-Net convolutional architecture inspired by [Wave-U-Net][waveunet].
The most recent version features hybrid spectrogram/waveform separation,
along with compressed residual branches, local attention and singular value regularization.
Checkout our paper [Hybrid Spectrogram and Waveform Source Separation][hybrid_paper]
for more details. As far as we know, Demucs is currently the only model supporting true
end-to-end hybrid model training with shared information between the domains,
as opposed to post-training model blending.

For detailed instructions on how to install, use and train Demucs,
checkout the [Demucs repository](https://github.com/facebookresearch/demucs).

## Dual U-Net Hybrid architecture

In order to add support for working at the same time in the spectrogram and waveform domain,
Hybrid Demucs uses a dual U-Net structure. The temporal branch gradually reduces the number of time steps,
while the spectral branch gradually reduces the number of frequency bins. After layer 5, the two representations
have the same shape and can be summed. The 6-th layer is shared bewteen the two branches.
The opposition happen in the decoder.

The output of the spectral branch is inversed to a waveform in a differentiable manner and summed
to the output of the temporal branch. The loss is thus always in the waveform domain and training
is completely end-to-end. The model is free to use combine both domains and exchange information
between them.

We provide hereafter a visual representation of the two branches U-Net structure.


```{figure} ../images/demucs/hybrid.png
---
alt: Schema representing the structure of Demucs, with a dual U-Net structure with a shared core, one branch for the temporal domain, and one branch for the spectral domain.
name: hybrid_demucs_schema
---
Dual U-Net structure of Demucs. The input waveform is processed
both through a temporal encoder, and first through the STFT followed by
a spectral encoder. The two representations are summed when their dimensions align.
The decoder is built symmetrically. The output spectrogram go through the ISTFT
and is summed with the waveform outputs, giving the final model output.
The 'Z' prefix is used for spectral layers, and 'T' prefix for the
temporal ones.
```

## Compressed Residual branches

Hybrid Demucs also features new compressed residual branches that increase the expressivity of the model and allow it
to handle long range context. Please refer to the paper for a detailed description of the content of those branches.

```{figure} ../images/demucs/residual.png
---
alt: Schema representing the residual branches in Hybrid Demucs, with dilated convolutions, biLSTM and local attention.
name: hybrid_demucs_schema
---
Representation of the compressed residual branches
that are added to each encoder layer. For the 5th and 6th layer,
a BiLSTM and a local attention layer are added.
```

## Results

We provide hereafter a summary of the different metrics presented in the [Hybrid Demucs paper][hybrid_paper].
You can also compare Hybrid Demucs (v3), [KUIELAB-MDX-Net][kuielab], [Spleeter][spleeter], Open-Unmix, Demucs (v1), and Conv-Tasnet on one of my favorite
songs on my [soundcloud playlist][soundcloud].

### Comparison of accuracy

`Overall SDR` is the mean of the SDR for each of the 4 sources, `MOS Quality` is a rating from 1 to 5
of the naturalness and absence of artifacts given by human listeners (5 = no artifacts), `MOS Contamination`
is a rating from 1 to 5 with 5 being zero contamination by other sources. We refer the reader to our [paper][hybrid_paper],
for more details.

| Model                        | Domain      | Extra data? | Overall SDR | MOS Quality | MOS Contamination |
|------------------------------|-------------|-------------|-------------|-------------|-------------------|
| [Wave-U-Net][waveunet]       | waveform    | no          | 3.2         | -           | -                 |
| [Open-Unmix][openunmix]      | spectrogram | no          | 5.3         | -           | -                 |
| [D3Net][d3net]               | spectrogram | no          | 6.0         | -           | -                 |
| [Conv-Tasnet][demucs_v2]     | waveform    | no          | 5.7         | -           |                   |
| [Demucs (v2)][demucs_v2]     | waveform    | no          | 6.3         | 2.37        | 2.36              |
| [ResUNetDecouple+][decouple] | spectrogram | no          | 6.7         | -           | -                 |
| [KUIELAB-MDX-Net][kuielab]   | hybrid      | no          | 7.5         | **2.86**    | 2.55              |
| **Hybrid Demucs (v3)**       | hybrid      | no          | **7.7**     | **2.83**    | **3.04**          |
| [MMDenseLSTM][mmdenselstm]   | spectrogram | 804 songs   | 6.0         | -           | -                 |
| [D3Net][d3net]               | spectrogram | 1.5k songs  | 6.7         | -           | -                 |
| [Spleeter][spleeter]         | spectrogram | 25k songs   | 5.9         | -           | -                 |


[hybrid_paper]: https://arxiv.org/abs/2111.03600
[waveunet]: https://github.com/f90/Wave-U-Net
[musdb]: https://sigsep.github.io/datasets/musdb.html
[openunmix]: https://github.com/sigsep/open-unmix-pytorch
[mmdenselstm]: https://arxiv.org/abs/1805.02410
[demucs_v2]: https://github.com/facebookresearch/demucs/tree/v2
[spleeter]: https://github.com/deezer/spleeter
[soundcloud]: https://soundcloud.com/voyageri/sets/source-separation-in-the-waveform-domain
[d3net]: https://arxiv.org/abs/2010.01733
[mdx]: https://www.aicrowd.com/challenges/music-demixing-challenge-ismir-2021
[kuielab]: https://github.com/kuielab/mdx-net-submission
[decouple]: https://arxiv.org/abs/2109.05418
[mdx_submission]: https://github.com/adefossez/mdx21_demucs