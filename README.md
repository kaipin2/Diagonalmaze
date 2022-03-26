# Diagonal-maze(以下Dm)をUnityで制作

実行環境 Unity 2019.3.14f1(64-bit)

このゲームは、自作したゲームルールを使って、Unityで作成したものである。  
ゲームは、迷路の亜種であり、プレーヤーは斜め移動しかできないようになっている。  
ゲーム盤上に数字が書かれているマスが存在するので、そのマスを数字の順番に通りながら最後にゴールを目指すゲームである。  
なお、数字と矢印が描かれているマスも存在し、そのマスを踏むと、矢印の向きに数字の分だけ強制移動する。  
※なお、移動させるキャラはス●イムである。

# 1.シーンの役割
**titleシーン**  
ゲームを開始したら一番初めに入るシーン。  
「ゲームを開始する」か「ゲームを終了する」か選ぶことができる 

**mainシーン**  
実際にゲーム(Dm)を行うシーン。  
ゲームが終了したら、titleシーンに戻るか、もう一度ゲームを行う(mainシーンにもう一回遷移)するか選ぶことができる

# 2.各スクリプトの役割
## 2.1 titleシーンのスクリプト
**2.1.1 Title Controller**  
titleシーンのメインスクリプト。  
titleシーンに配置されているボタンを押したときのActionを設定している  

**2.1.2 Title_Slime**  
titleシーンにぞんざいしているス●イム（キャラ）を制御するスクリプト。  
内容としては、反時計回りをするプログラムである。  

**2.1.3 Choice**  
titleシーンのボタンのうち、「Play」ボタンを選択した状態にするスクリプト。  

## 2.2 mainシーンのスクリプト
**2.2.1 CamereaMover**  
カメラ（視点）を動かすスクリプト。  
マウスを左クリックしながら動かすことで、視点が回転し、右クリックしながら動かすことで、前後左右に動く。  
また、キーボードでも視点を動かすことができる(s,x,c,zで前後左右に移動をし、q,e,で拡大縮小を行う)

**2.2.2 CreateMaze**  
迷路を作成するスクリプト。  
.txtのファイルから迷路の情報を取得し、その情報通りに迷路を構築する。  

**2.2.3 mainScript**  
mainシーンのメインスクリプト。  
ゲーム盤を生成し、カメラの位置やプレイヤーの位置を初期位置に設定する。  
また、キーボードの「１」が押されたとき、プレイヤーの前面を写すようにカメラを移動させ、  
「２」が押されたとき、プレイヤーの背面を写すようにカメラを移動させ、  
「３」が押されたとき、ゲーム盤を俯瞰視点で写すようにカメラを移動させる。  

**2.2.4 Mass**  
チェックポイントや強制移動するマスに効果ごとにテキストを付与するスクリプト。  
マスのObjectにある2つのテキスト欄にそのマスの効果を示すテキストを書き込む。  

**2.2.5 PlayerObject**  
ス●イム（キャラ）の動きを制御するスクリプト。  
右前、右後ろ、左前、左後ろの４方向の移動を制御している。  
※また、キーボードの「j」でジャンプすることができるが、特に意味はない。さらに、  
　ゲーム盤から落ちた時に復帰するスクリプトもあるが、意味はない。  

## 2.3 シーン内に登場しないスクリプト
**2.3.1 Buttons**  
ボタンが押されたときに起こすActionを保存しているスクリプト。  
ボタンのオブジェクトにコンポーネントし、クリックしたときに、Buttonsスクリプトの呼び出したい関数をあらかじめ保存しておく。  