# DeepStack

代表的な不完全情報ゲームである Poker(`Texas Hold'em`) においても、
DeepLearningがプロのプレイヤーに勝利

## Introduction

* 完全情報ゲーム、特に囲碁でのAIの勝利が記憶に新しい
* 不完全情報ゲームの `Poker` では、AIによる成功は、 `Heads Up Limit` に限られていた。
* `Heads Up Limit` における`Decision Point`は ~10^14
* 一方、囲碁の`Decision Point`は ~10^170  
* `Heads Up No Limit`(HUNL)の`Decision Point`は ~10^160 だからなんとかならないか？

* recursive reasoning of CFR
* intuition by DNN
* win rate: 4.5BB/100 (44,000 Hands)

## DeepStack

Recursiveな
1) `Continuous Re-Solving`
だけでは、計算量的にきつい。

その対策として、
2) `Limited Depth Lookahead via Intuition`
3) `Sparse Lookahead`

を行う。

2) `Limited Depth Lookahead via Intuition` は、
一定の深さで探索をやめて、事前学習したDNNによる
counterfactual valueで代替する。

counterfactual valueを計算するDNNは以下の構造
```
7-layer FFNN
(500nodes, ReLU on each layer)

Input:
* player's hand range
* opponent's hand range
* pot size
* public card
Output:
* player's hand value
* opponent's hand value

Output value が zero-sumの値となるような構造を追加
```

3) `Sparse Lookahead` は、
探索するActionを以下に制限することで、探索空間を絞る
* Fold
* Call
* 2Bet/Raise
* 3Bet/Raise
* All-In

## 疑問

DNNのInputとして、`各々のstack-size` or `effective stack-size`は入れなくていいのかな？
