# Pix2Pix

Image to Image な `Conditional GAN`

## Arhcitecture

* generatorへ直接的にノイズzを入れないで、stochasticなdropoutを行うことでノイズを注入
* 通常の`cGAN`のAdversarialなlossに加えて、L1-Lossも追加

* Generator: encoder-decoder with skip connections (`U-Net`)
* Discriminator: (`PatchGAN`)
```
L1-loss: 低周波成分を学習
Patch-GAN: 高周波成分を学習・・・NxN Patch に対して、Convolutionを行い、判定結果の平均をとる
```

- 低周波成分はL1-lossに任せているので、Patchで十分
- -> 少ないパラメータ、高速動作、任意サイズの画像に適応可能
