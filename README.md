# Slipe
真ん中にコマを寄せれば勝ち

## GUI play
`python -m game.gui`

## 強化学習について(案)
まず、基準として次のような入出力のモデルを作りたい。

### 盤面データの読み込みの方法
入力データは4 * 5 * 5の配列(今は`arr`と呼ぶことにする)で
- `arr[0]`は黒(キング以外)の位置
- `arr[1]`は白(キング以外)の位置
- `arr[2]`は黒キングの位置
- `arr[3]`は白キングの位置

という感じにしたい。

### 次の一手の出力の方法
1次元配列で次の多次元配列`next`を`flatten`したようなものにしたい。
- 各要素は次の一手の有効さを表す確率とする。
- `next[i, j, drc]`は、位置`[i, j]`のコマを`[drc]`の方向に動かす確率とする。
ただし、位置`[i, j]`は`GameState`を基準とし、`drc`は`Drc`の要素で方向を表す(どちらも`game/game_state.py`を参照のこと)。

動かし方としては、出力結果の手のうち、有効なものを確定的、あるいは確率的に選択する。

### モデル選択と学習方法
まずはAlpha GOのように、CNNとかで、モデルを作ってみるのがいいのかなあと。ただし、あんまり大きなモデルにはしないほうがよさげ。

学習については、はじめのうちはランダムな相手(`game/game_state.py`に作成済み)と戦わせて、勝てるようになってきたら、自分と戦わせるようかな？

その報酬については、勝利に対して点を与える感じかな、、？なんかもっと細かく点を与えたほうがいいのか、、？

あとは、モンテカルロ木探索とかやってみたいけど、とりま後回し？

