# 作品概要
目を模した多数の映像を空間内（天井）に配置し、人との距離やその動きによって視線を一斉に向けたりそらしたりする作品。
オブジェクトを天井から見下ろすように配置することで箱庭の中にいるような上位存在に観察されているような感覚のものができたら面白いのではないかと思います。
X Window systemの`xeyes`コマンドのようなイメージです。

## 目線の向きの計算
それぞれの目はプロジェクションマッピングで天井に投影し、個別に意識がどこに何パーセント向いているかというパラメーターを持たせます。
意識は人の動きがある方向により向けられ、人との距離が近いほど影響を強くします。
動きがなかったり少なかったりする間は意識がそれるようにします。
各方向への意識がどれくらい向いているかで重みづけされた確率でその瞬間ごとの目線を向けたい方向を決め、そちらに目線を移動させます。

## センサー/目/投影機の制御
人の動きの感知は同じく天井数か所にカメラ（から取得し一瞬前の映像フレームとの差分を計算して動きのあった場所を決めます。
目は一番近くのカメラからの情報を受け取るようにし、カメラごと（もしくはいくつかのカメラごと）に目とそれを投影する投影機で一つのグループとしてそれぞれ制御するのが良いと思います。（ボーダレスの世界のように複数のPCを同期させて目の位置も自由に動かせるともっと生き物のような不気味さを表現できると思いますが今の私の技術力では難しいと思うので発想だけにしておきます。）
あらかじめ位置が決まっていれば目のクラスのコンストラクタで投影機との位置関係をパラメータとして受け取るようにしてインスタンス作成時に投影時のゆがみを補正するための補正値を計算しておけるので計算量は減らせるかと思います。

## 発展
可能であれば人の動きを感知するセンサーを赤外線などにし、天井ではなく空間内に球状オブジェクトを配置してそこに投影することでいわゆる黒目の部分だけではなく目自体を動かすといった表現ができるので、より視線を集めている感覚は強く感じられると思います。
目の動きをある閾値を超えたときだけ速くそちらへ動かしそれ以外はゆったりと動かすことでより人の目線の動かし方に近く、視線を集めたという感覚が強くなると思います。
黒目は少し間隔をあけて（センサーのフレーム間隔よりも長い間隔で）動きの有無を計算して直線的に一瞬前向けていた場所から次に向ける場所へと素早く動かす。
目自体はある程度ゆったりと常に（細かい間隔で動かす方向を計算して）動かし、黒目はその目の位置をベースにした相対位置を計算するようにする。


より有機的な動きにするのには黒目と目自体の動きをどう表現したらよいかや、動かすときに一瞬前の地点と次の地点をどのように（速度、軌道等）結ぶかについてはトライアンドエラーが必要だと思います。  
~~あまり具体的に考えられていませんがよろしくお願いします。~~
