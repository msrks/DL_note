#### 2017-1
[DeepStack: Expert-Level Artificial Intelligence in No-Limit Poker](notes/deep-stack.md)[[arxiv](https://128.84.21.199/pdf/1701.01724)]

#### 2016-12

[Modeling documents with Generative Adversarial Networks  ](notes/adversarial-document-model.md)[[arxiv](https://arxiv.org/abs/1612.09122)]

[Plug & Play Generative Networks: Conditional Iterative Generation of Images in Latent Space](notes/ppgn.md)[[arxiv](https://arxiv.org/abs/1612.00005)]

#### 2016-11

[Image-to-image translation using conditional adversarial nets](notes/pix2pix.md)
[[arxiv](https://arxiv.org/abs/1611.07004)]

#### 2016-6

InfoGAN: Interpretable Representation Learning by Information Maximizing Generative Adversarial Nets[[arxiv](https://arxiv.org/abs/1606.03657)]

* http://www.inference.vc/infogan-variational-bound-on-mutual-information-twice/
```
- （infoじゃない）GANの損失関数も、相互情報量を使って定式化できる
- GANの損失関数は、相互情報量の下限に対応する
- 本来は上限をminimizeすべきなので、これがGANの学習の不安定性に対応しているのでは？
- info GANの2項目にvariational boundを適用すると下限に対応するので
全体を合わせるとよくわかんないことになってる
```

#### 2016-3

Adaptive Computation Time for Recurrent Neural Networks [[arxiv](https://arxiv.org/abs/1603.08983)]

#### 2015-11

Neural Programmer: Inducing Latent Programs with Gradient Descent [[arxiv](https://arxiv.org/abs/1511.04834)]

#### 2015-4

Anticipating Visual Representations from Unlabeled Video
[[arxiv](https://arxiv.org/abs/1504.08023)]
```
- future frame の カテゴリ を予測する（フレームそのものではない）
- 事前学習したCNNの隠れ層表現を予測する
- multi-outputを予測して、もっともうまく予測できたものの予測誤差が最小となるように学習する
```
