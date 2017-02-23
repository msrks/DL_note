## Notes on "Unsupervised Represerntation Learning by Solving Jigsaw Puzzles" · April 28th, 2016

画像用NNの新しい斬新な初期化方法（ジグソーパズルを解かせる）[[arxiv.16.03](https://arxiv.org/abs/1603.09246)]に対する考察。
ちなみに、画像用NNの初期化は 別のdatasetに対して教師ありしたNNを使って、transfer learningを行うのが常套手段で state-of-the-art。一方、このジグソーパズルを解かせる方法は、`教師なしNNを使った初期化方法`として state-of-the-art。denoising AE と考え方が似てるが（ジグソーパズル並べ替えもある種のdenoising）最後に書くように、生成モデル的な考察をすると、より効率的なことがわかる（生成のためには必要でも、判別のために不要な表現は学習しない）

ジグソーパズルの損失関数
```
    Loss ~ - EV_x~p[log(f(x)) + log(1-f(x^))]
```
をminimizeするために、CNNが内部で生成モデルQ(x)を学習していると仮定して、
じゃあどんな生成モデルQ(x)を学習しているのかを考えると、Q(x)は以下の損失関数を最小化するように学習することがわかる
```
    Loss ~ KL(P||Q) - KL(P+P^/2||Q+Q^/2)
```
つまり、Pに似た分布のQは学習したいけど、x^に対してP^が小さくなることはQ^学習しなくていいということになる。（いまいち納得しかねる結果・・）ラベル判別タスクのためには、本当の生成モデルほどしっかりPを学習しなくてよくて、ジグソーパズルタスクを使った初期化はここのところが上記の目的に合致するので、ジグソーパズルタスク学習によるtransfer learningがうまくいったと説明。これが denoising AEとの差。

## Adversarial Preference Loss · March 25th, 2016

Discriminatorはペア(2つ)の入力をとる。どちらか一方がrealで、もう一方がfake。
どちらがrealらしいかを判定するように学習する。

このformulationでは、KL-div.に収束する形のGANになる

## An Alternative Update Rule for Generative Adversarial Networks · March 21st, 2016

JS-div.ではなく、KL-div.に収束する形のGANのupdateルールの話

## Deep Learning is Easy - Learn Something Harder · January 25th, 2016

Deep Learning を研究するための心得。表面的に薄っぺらくじゃなくて、Something Harderを学ぶべし

## The Next Episode: I'm joining Magic Pony Technology · January 8th, 2016

## Adversarial Autoencoders (vs Moment Matching Autoencoders?) · January 8th, 2016

## Accuracy vs Explainability of Machine Learning Models [NIPS workshop poster review] · December 22nd, 2015

## When is Machine Learning Worth it? · November 24th, 2015

だいたいの問題は、ヒューリスティックスを使ったり、せいぜいlogistic regressionで十分。この分野へのMLの適用はすでにsaturateした部分の性能をわずかに向上させるだけ。本当にMLが有用な領域は、speech recongnitionシステムみたいに、>95%の精度じゃないと製品にならないような基準がある場合。この場合は 0を1にすることができ、MLが大活躍する。

## How to Train your Generative Models? And why does Adversarial Training work so well? · November 17th, 2015

infinite data かつ perfect model の下では、生データの分布をP、生成モデルをQとして、KL(P||Q)もKL(Q||P)も同一分布(Q=P)に収束するが、finite data や model misspecification の下では、異なった振る舞いをする。

* KL(P||Q)の場合には、over generalizeする。

QはPの分布全範囲を無理に再現しようとして、非現実的なサンプルを生み出す

* KL(Q||P)の場合には、under generalizeする

QはPの分布全範囲を再現するのを諦めて、一部分のみに対して正しく生成しようとする

その結果、対数尤度的には KL(P||Q)の方が有利だが、KL(Q||P)の方がより自然なものを生成できる。ちなみに、naive-GANは、JS(P||Q) ~ KL(P||P+Q/2)/2+KL(Q||P+Q/2)/2を最小化してる。一方、VAEやAutoRegressiveモデルはKL(P||Q)を最小化してる。

* 補足：KL(P||Q) 最小化が 対数尤度最大化と同値であることのメモ

min KL(P||Q)
~ min Sigma(PlogP – PlogQ)
~ min Sigma( - PlogQ)
~ max Sigma(PlogQ)
~ max E_P[logQ]

## Idea of the Week: Maximum Spacing Estimation, Gaussianisation and Autoregressive Processes · October 22nd, 2015

## A Word of Caution on Scheduled Sampling for Training RNNs · September 11th, 2015

系列を出力するNNの training と inference の環境の違いを埋めるための技術、
Scheduled Sampling for Sequence Prediction with Recurrent Neural Networks [[arxiv.15.06](https://arxiv.org/abs/1506.03099)] に対する考察

Strictly proper scoring rules を scheduled sampling は満たしておらず、eplison=0にした時の収束解は、直前までの系列を完全に無視するモデルとなることを指摘。adversarial training もしくは generative moment matchingの方がいいと提案。
