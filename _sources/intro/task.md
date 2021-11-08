Task
==============

The task of the Music Demixing (MDX) Challenge is *music demixing*, which is a special case of *source separation*.

## Source Separation
Source separation is the process of isolating individual sounds in an auditory
mixture of multiple sounds {cite}`vincent2018audio,cano2018musical,rafii2018overview` 
, as defined in the [previous tutorial](https://source-separation.github.io/tutorial/intro/src_sep_101.html)
{cite}`opensourceseparation:book`.

Mathematically, we assume that a mixture signal $y(t)$ consists of $N$ sources, 
$x_n(t)$, for $n=1...N$, such that

$$
y(t) = \displaystyle\sum_{i=1}^{N} x_i(t).
$$

Source separation is the inverse operation of the mixing process.
We aim to find the original signals, $x_n(t)$ for $n=1...N$, for a given mixture signal $y(t)$.


## Music Demixing

Music Demixing (MDX) is a special case of Source Separation. 
A given mixture signal is a song, and source signals are sounds from musical instruments.

```{image} ../images/source_separation.png
---
alt: Music Demixing.
```

Recently, many data-driven approaches have been proposed for music demixing.
Especially, deep learning methods {cite}`kong2021decoupling,lin2021unified,choi2020,liu2020,takahashi2020d3net,spleeter2020,defossez2019music,defossez2019demucs,lluis2019end,choi2021lasaft`
have become mainstream because they have shown outstanding performance.


To train a deep neural network for music demixing, we need a training dataset.
We explore datasets for music demixing in the following section.



