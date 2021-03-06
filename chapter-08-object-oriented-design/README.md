# オブジェクト指向

方針:

1. 曖昧さをなくす
    * いつ
    * どこで
    * だれが
    * なにを
    * なぜ
    * どうした  
2. コアとなるオブジェクトを定義する
3. オブジェクト同士の関係を定義する
4. 各オブジェクトのキーとなるアクティビティを定義する


## 8-1. ブラックジャックのゲームを設計

`src/black_jack.coffee`

初期設定まではできたはず・・・  
設計ではなくなってしまった  
必要なクラスの洗い出しまではできているはず・・・

TODO ループしてプレーヤーごとにターン回したり、終了時の勝敗判定が必要

## 8-2. コールセンター業務をシミュレーション

`src/call_center.py`


## 8-3. ジュークボックスの設計

### やること

<table>
  <tr> <th>いつ</th> <td>-</td> </tr>
  <tr> <th>どこで</th> <td>-</td> </tr>
  <tr> <th>だれが</th> <td>誰か</td> </tr>
  <tr> <th>何を</th> <td>ジュークボックス</td> </tr>
  <tr> <th>なぜ</th> <td>音楽を聞きたいから</td> </tr>
  <tr> <th>どうする</th> <td>CDを選択して再生する</td> </tr>
</table>

### フロー

1. コインを投入する
2. コインが規定の金額になったら、CDの選択を可能にする
3. CDが選択されたらお釣りを返す。
4. 選択されたCDをプレーヤーに突っ込む(ジュークボックスが)
5. CDを再生する(プレーヤーが)
6. 再生中にCDが選択されたらプレーリストに登録する
7. CD再生終了を通知(プレーヤーからジュークボックスへ)
8. プレーリストが空でない場合は再び手順5から

今回はめんどくさいのでコイン1枚でOKとし、3の手順ははぶく

### 登場人物と役割

Operator: ジュークボックスを操作する人  
動作

* コイン投入
* CD選択

Jukebox: ジュークボックス  
変数

* CDリスト

動作

* コインが規定の金額になったらCD選択可能にする
* CDをプレーヤーに装填(再生中であればプレーリストへ)

CD: CD  
変数

* 再生秒数

Player: CDプレーヤー  
変数  

* プレーリスト
* 再生状態


動作

* 再生

## 8-4. 駐車場の設計

### やること

<table>
  <tr> <th>いつ</th> <td>-</td> </tr>
  <tr> <th>どこで</th> <td>-</td> </tr>
  <tr> <th>だれが</th> <td>運転手/td> </tr>
  <tr> <th>何を</th> <td>車</td> </tr>
  <tr> <th>なぜ</th> <td>車を止めたいから</td> </tr>
  <tr> <th>どうする</th> <td>駐車する</td> </tr>
</table>

### フロー

1. 車が来る
2. 満車かどうか確認
3. 入り口のバーを開ける
4. 車が通ったらバーを閉じる
5. 車を空きスペースに止める
6. 時間計測スタート
7. 一定時間経過後、車を出す
8. 金額を計算する
9. バーが開く
10. 車が通ったあとバーを閉じる

* 車と駐車時間を対応付ける必要がある
* 満車かどうか確認

### 登場人物と役割

Car: 車  
変数  

* 駐車場のID

動作  

* 駐車する(ID取得)

ParkingLot: 駐車場  
変数  

* 駐車スペース
* 入り口と出口のバー
* 売上
* 満車フラグ

動作  

* バーの上げ下げ管理
* 売上計算

ParkingSpace: 駐車スペース  
変数  

* ID
* 駐車時間

Bar: 入り口出口のバー  

変数  

* 閉じてるか開いているか

動作  

* 閉じる開ける

## 8-5. オンラインブックリーダーの設計

### やること

<table>
  <tr> <th>いつ</th> <td>-</td> </tr>
  <tr> <th>どこで</th> <td>ネットで</td> </tr>
  <tr> <th>誰が</th> <td>アカウントを持ってる人</td> </tr>
  <tr> <th>なにを</th> <td>本</td> </tr>
  <tr> <th>なぜ</th> <td>ネット環境があればいつでもどこでも読めるから</td> </tr>
  <tr> <th>どうする</th> <td>読む</td> </tr>
</table>

### フロー

1. アカウント作成
2. ログイン
3. 購入した本の一覧
4. すべての本から検索
5. 本の購入
6. 本の閲覧


### 登場人物と変数

Book: 本

* ISBN
* タイトル
* コンテンツ
* 著者名
* 価格
* ページ数

User: ユーザー

* ユーザー名
* パスワード
* ログイン状態
* 本棚
* Viewer

BookShelf: ユーザーの本棚

* 本(n)

MarketPlace: 本売り場

* 本(n)


Viewer: 本閲覧ツール

* 閲覧中の本
* 閲覧中のページ番号
* しおり

## 8-6. ジクソーパズルの設計と実装

`src/jigsaw.py`

### 遊び方

1. パズルのピースをシャッフルする
2. パズルのピースを選択する
3. 選択したピースを任意の位置にはめ込む
4. すべてのピースが正しい位置に配置されたらOK

ユーザはピースを正しい位置に置いたかどうかは最後まで判定するすべはないが、  
ピースの組み合わせが正しいかどうかはfitsWithメソッドで判定することができる。


### 登場人物

JigsawPuzzle: パズルのフレーム  
変数  

* パズルのピース

機能  

* ピースをシャッフルする
* パズルが完成したかどうか判定する

Piece: ピース

変数  

* 上下左右のピースID 
* 上下左右がFit済みかフラグ

機能  

* Fitするかどうか判定

Player: プレイヤー  
機能  

* ピースを選択する
* ピースをはめ込む


## 8-7. チャットサーバの設計と懸念点

### やること

<table>
  <tr> <th>いつ</th> <td>-</td> </tr>
  <tr> <th>どこで</th> <td>-</td> </tr>
  <tr> <th>誰が</th> <td>友達同士</td> </tr>
  <tr> <th>なにを</th> <td>メッセージ</td> </tr>
  <tr> <th>なぜ</th> <td>コミュニケーションを取りたいから</td> </tr>
  <tr> <th>どうする</th> <td>やりとりする</td> </tr>
</table>

### フロー

1. ユーザー登録
2. ログイン
3. 友だちを探す
4. 友達リクエストを送る
5. チャットする友達を選択する(複数可)
6. サーバにメッセージを送る
7. サーバはメッセージを受信
8. サーバは友達にメッセージを送る


### 懸念点

* オンラインかどうかどう確認するか? ping的なもの？
* スケールした時にメモリ上の情報を他のサーバとどう共有するか。また共有必要があるか


## 8-8. オセロの設計と実装

### フロー

1. 8x8のボードを用意
2. 64枚のピースを用意
3. プレーヤー二人を用意
4. うち32枚を黒、32枚を白にしてプレーヤーに配る
5. 白黒2枚ずつをボードの真ん中へ設置
6. ボードをDisplayする
7. ユーザーインプットを待機
8. インプットをパース
9. ピースを置く
10. 白黒ひっくり返す
11. 次のプレーヤーが置く場所があるか確認。あれば5-10を繰り返す
12. 枚数を数えて勝者を決定

### 登場人物

* Board
    * 初期化処理
        * 8x8 array
        * 2 players
        * 32B, 32W pieces
        * 4枚を真ん中に配置
        * Promptの初期化
        * 30枚ずつをPlayerに配布
    * ボードの再描画処理
        * Promptへ制御を渡す
    * 挟まれたピースの反転
    * 置き場所の確認
    * 終了処理
        * 枚数をカウントし勝者を決定
        * Byeを描画
* Player
    * pieces
    * ピースを置く
* Piece
    * 白か黒
* Promt
    * インプットを促す
* CommandParser
    * コマンドの解析

## 8-9. in-memoryファイルシステムの設計

* ファイル／ディレクトリ／リンク
* 権限rwx(ユーザーやグループはなし)
* ツリー構造
* ルート
* ファイルメタ情報(ファイル名、コンテンツ、作成日、修正日、パーミッション)
* 作成,編集,削除,情報表示するコマンド

### 登場人物

* FileSystem
    * rootディレクトリ
    * カレントディレクトリの参照
    * Promptの初期化
* Path
    * 絶対パス相対パスの解釈
* Entry
    * ファイル名
    * 作成日
    * 修正日
    * パーミッション
* File extends Entry
    * コンテンツ
* Directory extends Entry
    * Entryリスト
* Link extends Entry
    * 実体への参照
* Prompt
    * コマンドの入力受付
    * コマンドのパース
* Command
* CdCommand extends Command
    * Directory名を引数として受け付ける
    * FileSystemのカレントディレクトリをDirectoryに変更する
* LsCommand extends Command
    * Entry名を引数として受け付ける
    * Entryの情報を表示
* CatCommand extends Command
    * File名, Link名を引数として受け付ける
    * Fileの内容を表示
* TouchCommand extends Command
    * File名を引数として受け付ける
    * Fileを作成
* MkdirCommand extends Command
    * Directory名を引数として受け付ける
    * Directoryを作成
* LnCommand extends Command
    * Link名とFile名もしくはDirectory名を引数として受け付ける
    * Linkを作成
* EchoToFileCommand extends Command
    * 引数として文字列,File名を受け付ける
    * Fileのコンテンツの編集
* RmCommand extends Command
    * 引数としてEntry名を受け付ける
    * Entryの削除


## 8-10. Hashtableの実装

`src/hashtable.py`

### やること

とあるキーをハッシュ化してMapに格納。  
キーが衝突した場合はlinkedlist形式でつるしていく。  

挿入、更新、参照、削除ができればよいとする。

### フロー

挿入  

1. key、valueを受け取る
2. keyをhashing
3. hashされたkeyがすでに存在するか確認
4. hashの位置にkey, valueを格納する
    1. hashが存在していない場合は、新しいlinkedlistを作り、key,valueを格納する
    2. hashが存在している場合は、linkedlistに新しい要素を作成し、key,valueを格納する

更新

1. key、valueを受け取る
2. keyをhashing
3. hash位置にあるlinkedlistを取得
4. 前から順番にkeyがあるか探してく。
5. 発見したらvalueを上書き

参照

1. keyを受け取る
2. keyをhashing
3. hash位置にあるlinkedlistを取得
4. 前から順番にkeyがあるか探してく。
5. 発見したvalueを返す。

削除

1. keyを受け取る
2. keyをhashing
3. hash位置にあるlinkedlistを取得
4. 前から順番にkeyがあるか探してく。
5. 要素を削除して、前の要素に次の要素のポインタを渡す

## LinkedList

双方向LinkedListにする。  
前の要素と次の要素とコンテンツを持つ。  
先頭は前の要素はNone、末尾は次の要素がNone
