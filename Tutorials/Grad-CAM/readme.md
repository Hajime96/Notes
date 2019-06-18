# Grad-CAM(Gradient-weighted Class Activation Mapping)

### Indexing:
  - [Introduction](#Introduction)
  - [Method](#Method)
  - [References](#References)

---
### Introduction
**Abstract**
- 機械学習，特に，深層学習は判断結果・根拠の解釈が難しい，つまり，なぜそのように判断したのかの根拠が示されない(**ブラックボックス**)という問題点がある．とりわけ，畳み込みニューラルネットワーク(CNN)は，画像から対象物を判別する時，画像のどこに着目しているのかを知りたい．
- CAMやGrad-CAMは，CNNが，どこに注目をして判断したのかを可視化できるツールである．
---
### Method 
- まず，Grad-CAMの仕組みを押さえておく．Grad-CAMの概要図を下図に示す．畳み込みニューラルネットワーク(CNN)は，畳み込み層とプーリング層を何層にも積み重ね特徴を抽出する部分とその特徴量出力を受け取りクラスラベルと照合して，教師あり学習を行う識別部分がある．識別部分は，全結合の多層ニューラルネットワーク(全結合層)で構成され，その最終層は特徴量を各クラスの確率スコアに変換するsoftmax層になっている．確率スコアとは，入力画像に各クラスのタグが付与される確率のことを指す。例えば，犬と猫の2値分類の場合，入力画像に対して"犬"が付与される確率が90％、"猫"が付与される確率は10％と計算されたとすると，判定結果は，確率スコアが最大となるクラスとなるため，この場合の予測結果は，"犬"がタグ付けされる．
<img src="https://github.com/Hajime96/Notes/blob/master/Tutorials/images/gradcam-figure.png" width="1245" hegiht="571" align=center/>
  
  1. Pre-training AlexNetやVGGを用いて入力画像の推論を行う
  2. 対象となるクラスのみ1，それ以外を0として逆伝播を行う
  3. 各チャンネルで勾配のGlobal Average Pooling(GAP)を計算し，それを重みとする
  4. 特徴マップの値に重みを掛け，足し合わせてReLUに通す
  
---
### References
- [Grad-CAM: Visual Explanations from Deep Networks via Gradient-based Localization](https://arxiv.org/pdf/1610.02391.pdf)
- [Grad-CAM++: Improved Visual Explanations for Deep Convolutional Networks](https://arxiv.org/pdf/1710.11063.pdf)

