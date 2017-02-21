### Notes on "Unsupervised Represerntation Learning by Solving Jigsaw Puzzles" · April 28th, 2016

画像用NNの新しい斬新な初期化方法（ジグソーパズルを解かせる）[arxiv](https://arxiv.org/abs/1603.09246)に対する考察。
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

### Adversarial Preference Loss · March 25th, 2016

Discriminatorはペア(2つ)の入力をとる。どちらか一方がrealで、もう一方がfake。
どちらがrealらしいかを判定するように学習する。

このformulationでは、KL-div.に収束する形のGANになる

### An Alternative Update Rule for Generative Adversarial Networks · March 21st, 2016

JS-div.ではなく、KL-div.に収束する形のGANのupdateルールの話

### Deep Learning is Easy - Learn Something Harder · January 25th, 2016

Deep Learning を研究するための心得。表面的に薄っぺらくじゃなくて、Something Harderを学ぶべし
