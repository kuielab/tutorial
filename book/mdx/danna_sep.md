# Dana-Sep

Danna-Sep is a combination of three different models: X-UMX, U-Net, and Demucs. Each sub-models has been modified either by training with a different objective, or by introducing some architecture changes. The final output is a linear combination of individual outputs from the sub-models. To know the exact settings and details about our model, please checkout our paper [**Danna-Sep: Unit to Separate Them All**](https://s3.eu-west-1.amazonaws.com/production-main-contentbucket52d4b12c-1x4mwd6yn8qjn/db5ef2bf-b28e-4596-b449-baa533044314.pdf) presented in the MDX21 workshop at ISMIR.

```{figure} ../images/danna/diagram.jpg
---
alt: 
name: danna_sep_schema
---
The schematic diagram of Danna-Sep.
```

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

### Training


## Contact

* Email: ya70201@gmail.com
* Github/Twitter: @yoyololicon