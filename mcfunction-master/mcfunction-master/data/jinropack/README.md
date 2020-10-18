# jinropackについて
　マイクラ人狼を行うためのfunctionです．このfunctionを使えばゲームマスターを用意することなくマイクラ人狼ができます．

　このfunctionは通常のサバイバルワールドで動かしても問題がないようになっています．また，一部のプレイヤーがサバイバルモードをプレイしている時に，他プレイヤーがこのfunctionを使いマイクラ人狼を行っても問題が起きないような設計になっています．
ただし，マイクラ人狼中サバイバルモードでは以下のようなことが起きます．
- Mobがスポーンしない
- deathメッセージが表示されない
- 死亡してもインベントリの中身がキープされる

　functionやコマンドが何かよくわからない人は[このサイト](https://modern-craft.info/function/premite/)で簡単に理解できます．

## 前提
　チートの許可がonになっているワールドが前提です．

　また，実際にマイクラ人狼の戦いが繰り広げられる場所(ステージ)と，ゲームのセッティングや，勝敗が決まった際にプレイヤーたちが集合する場所(待合所)が用意されている必要があります．

　そのほかに以下のような条件があります
- Minecraftバージョン：1.14〜
- 最大プレイヤー数：15

## マイクラ人狼について
　[動画](https://www.youtube.com/watch?v=jWjh9-l2JIw&t=1s)を見るのがわかりやすいと思います．
プレイヤーは人狼陣営と村人陣営に別れて戦います．両陣営とも，相手陣営を全滅させることが勝利条件です．
プレイヤーは全員が役職を持ちます．ただし，誰にどの役職かは本人しかわかりません．
- **村人陣営**
  - 村人：特殊な能力なし
  - 占い師：死亡していない他のプレイヤー誰か一人を選択し，その陣営を知ることができる．死亡している場合はわからない．
  - 霊媒師：死亡している他のプレイヤー誰か一人を選択し，その陣営を知ることができる．死亡していない場合はわからない．
- **人狼陣営**
  - 人狼：人狼が複数いる場合，誰が人狼かわかる．
  - 狂人：占い師や霊媒師に占われた時，村人陣営と表示される．

　また，全てのプレイヤーに以下のアイテムが配布されます．
- 必殺の剣：一撃でプレイヤーを殺害する剣
- 必殺の弓：一撃でプレイヤーを殺害する弓
- 矢(64本)
- パン(12コ)

　なお，死亡したプレイヤーはその時点から声を出すことが禁止されます．
## まず初めに
### 環境構築コマンド
　このfunctionを導入したら，まず初めに以下のコマンドを実行させましょう．

``/function jinropack:status_setting/init``

　このコマンドは一度実行すれば今後は行う必要はありません．
### functionの書き換え
　自分のワールドに合うように，一部の座標を書き換えなければいけません．

　「jinropack」内の「stage1」の中にある「tp.mcfunction」を開き，２つある``x y z``をどちらもステージの入り口のx座標，y座標，z座標に書き換えましょう．

　次に同じフォルダ内にある「set_aftp_block.mcfunction」を開き，``x y z``を以下の条件に合うx座標，y座標，z座標に書き換えましょう．
- ステージの近く
- プレイヤーの目に入らない
- 上に2ブロックぶん開きがある

恐らくステージの上空なんかがいいのではないでしょうか．

　最後に「jinropack」内の「game」の中にある「end.mcfunction」を開き，２つある``x y z``をどちらも待機所のx座標，y座標，z座標に書き換えましょう．
## ゲーム開始までの流れ

### 設定変更
　以下のコマンドを実行してゲーム設定を変更します

``/function jinropack:status_setting/start``

### マイクラ人狼へのプレイヤーの参加
　ゲームに参加するプレイヤー全員に以下のコマンドを実行させましょう．

``/function jinropack:status_setting/join_jinro``

**また，ゲーム開始時に手持ちのアイテムは全て消えてしまうため，防具等も含めチェストに預けるようにしましょう**
### 役職の設定
　本functionではあらかじめ人数にあった役職を設定するコマンドを用意しています．
人数ごとの内訳は以下の通りです．

|人数|人狼|狂人|占い|霊媒|
|---|----|---|-----|-----|
|4|1|0|1|0|
|5|1|1|1|0|
|6|2|0|1|1|
|7|2|1|1|1|
コマンドはそれぞれ以下です．
- 4人：``/function jinropack:jobs/4``
- 5人：``/function jinropack:jobs/5``
- 6人：``/function jinropack:jobs/6``
- 7人：``/function jinropack:jobs/7``

また，数を一人ずつ設定することができます．ただし，以下で設定できる人数は，各役職5人までです．
- 人狼：``/function jinropack:jobs/jinro``
- 狂人：``/function jinropack:jobs/kyojin``
- 占い：``/function jinropack:jobs/seer``
- 霊媒：``/function jinropack:jobs/phyc``

役職の設定を間違えた場合は以下のコマンドでリセットし，初めから設定しなおします．

``/function jinropack:jobs/reset``

### アイテムの設定
　デフォルトのアイテム加え，特別なアイテムをランダムに一人配布することができます．アイテムは以下の6つであり，それぞれ対応するコマンドによって配布することを設定できます．
- エンダーアイ：``/function jinropack:items/ender``
- エリトラ：``/function jinropack:items/elytra``
- 盾：``/function jinropack:items/shield``
- 不死のトーテム：``/function jinropack:items/totem``
- 透明化のポーション(10秒)：``/function jinropack:items/invisible_p``
- 必殺のスプラッシュポーション：``/function jinropack:items/kill_p``

全てのアイテムを配布したい場合以下のコマンドを使用します．

``/function jinropack:items/setall``

複数のアイテムが設定された場合，それぞれ重複しないようにランダムなプレイヤー1人ずつに配布されます（1人が2つ以上のアイテムを受け取ることはありません）．

アイテムの設定を間違えた場合は以下のコマンドでリセットし，初めから設定しなおします．

``/function jinropack:items/reset``

### ゲーム開始
　以上の設定が全て終了したら，以下のコマンドでゲームを始めます．

``/function jinropack:stage1/start``

連続してマイクラ人狼を行う場合，役職やアイテムに変更がなければこのコマンドをもう一度実行することでできます．
役職やアイテムを変更する場合は上記の手順に沿って一度リセットし，設定し直します．

## ゲーム終了・途中離脱
　途中離脱するプレイヤーには以下のコマンドを実行させます．

``/function jinropack:status_setting/exit_jinro``

またマイクラ人狼が完全に終了した際には，以下のコマンドを実行してゲーム設定を通常に戻します．

``/function jinropack:status_setting/end``

## 複数ステージの登録
複数ステージを扱いたい場合は以下の処理をしてください．
1. 「stage1」のフォルダを，同じ場所に「stage2」という名前で複製する．
1. 「stage2」の中にある「start.mcfunction」に書いてある``stage1``を全て``stage2``に変更する．
1. 「stage2」の中身について，上記の"functionの書き換え"に従い座標を書き換える．

この作業により，以下のコマンドで二つ目のステージにてゲームを始められます．

``/function jinropack:stage2/start``

同様の手順でステージを無制限に増やすことができます．
## 禁止事項
スペクターモードになっているプレイヤーがわかってしまうため，tabキー(プレイヤーリスト)は禁止しています．今の所良い対策法がないため良心に頼る形になっています．