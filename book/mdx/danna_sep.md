# Dana-Sep

Danna-Sep is a combination of three different models: X-UMX, U-Net, and Demucs. Each sub-model has been modified either by training with a different objective, or by introducing some architecture changes. The final output is a linear combination of individual outputs from the sub-models.

## Multi-Domain Inputs

The reason why we adopted a combinational approach is because it is known that source separation models which use spectrogram as inputs are effective on harmonic sources such as vocals, while those which use audio as inputs are effective on percussive sources such as drums. We aimed to combine the best of both worlds in our model. Below is the system diagram of our model.


```{figure} ../images/danna/diagram.jpg
---
alt: 
name: danna_sep_schema
---
The schematic diagram of Danna-Sep.
```

To know the exact settings and details about our model, please checkout our paper [**Danna-Sep: Unit to Separate Them All**](https://mdx-workshop.github.io/proceedings/chinyun.pdf) presented at the MDX workshop in ISMIR 2021.

## Experimental Results

We trained Danna-Sep on the training set of MUSDB18-HQ, and tested it on the test set of MUSDB18 using [museval](https://github.com/sigsep/sigsep-mus-eval). The SDR results are presented below.

|         | Drums | Bass | Other | Vocals | Avg. |
|---------|:-----:|:----:|:-----:|:------:|:----:|
| X-UMX (baseline) | 6.44 | 5.54 | 4.46 | 6.54 | 5.75
| X-UMX (ours) | 6.71 | 5.79 | 4.63 | 6.93 | 6.02
| U-Net (ours) | 6.43 | 5.35 | 4.67 | 7.05 | 5.87
| Demucs (baseline) | 6.67 | 6.98 | 4.33 | 6.89 | 6.21 
| Demucs (ours) | 6.72 | 6.97 | 4.4 | 6.88 | 6.24
| Danna-Sep | **7.2** | **7.05** | **5.2** | **7.63** | **6.77**

It's clear that our modifications to the baseline models indeed improve the performance, and by combining those models, Danna-Sep surpass all baselines by a large margin and achieve the state-of-the-art performance.

## Resources

### Inferences

We provide a pre-trained Danna-Sep as a python package and can be used as a command line tool, so user can separate there favorite songs using one simple command. 
The installation instructions are available [here](https://github.com/yoyololicon/danna-sep).

### Training

If you want to redo our experiments, or want to train Danna-Sep on your own datasets, please checkout our [repository](https://github.com/yoyololicon/music-demixing-challenge-ismir-2021-entry). To use your own trained checkpoints, please install the [inference tool](#inferences) first, then follow the instructions in the repository README.


## Contact

* Email: ya70201@gmail.com
* Github/Twitter: @yoyololicon