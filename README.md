# スマートフォンアプリ開発Bの授業資料

## テーマ：ハイブリッドアプリの作成
* Apach Cordova を使用したハイブリッドアプリの作成を行います
* ネイティブアプリとのコードの比較や，実際の使用感の違いも確かめていきましょう

## 授業参加にあたっての注意点
* 大前提として休まないこと。1/3以上の欠席がある場合は単位取得の意思なしとみなします。ただし，やむを得ぬ事情で欠席する場合は，事前にメールにて連絡してください
* JavaScript, HTML, CSS の扱いに関して，手厚くフォローすることはできないと思います。各自復習をしておいてください。担当教員の違いなどで過去の授業の進捗，内容にずれが生じている可能性もあります（jQueryの扱いなどがそれに当たります）。そのような点に関しては授業中にできる限りフォローする予定です。
* 実習機はMacです。ios アプリのテストを行いたいWindowsユーザーは実習機を有効活用してください。
* 実習機のみで授業をこなすことはできますが，家のPCに開発環境が構築できていなければ，課題に支障が出る可能性があります。開発環境の構築に関しては2回目の授業でしか実施しません（もちろん質問には随時お答えしますが）。計画的に授業に参加してください。
* 授業ではコマンドラインでの操作をメインに行いますが，統合開発環境の利用や，Monaca などの利用もOKです。その際は自身で情報を収集して作業してください。

## 課題に関して
* 課題のファイル名は半角英数のみを使用してください
* 課題が締め切りに間に合わなかったとしても，必ず出来上がっているところまでを提出してください。提出してくれなければ採点（評価）のしようがありません
* 課題は他人の丸写しをしないでください。しんどいかもしれませんが，自分の頭で考え，自分の指で出力することが大切です
* 教え合うことは大歓迎です。
* 課題の内容をこなすことに満足するのではなく，その先のこだわりを見せてください。頑張れば頑張っただけ，評価したいと思っています

## 第1回　実力テスト, ハイブリッドアプリ#1
1. JavaScript でのクリックイベントとalertの表示
2. HTML5/CSS3 でのスマホ用画面の設計と実装
3. JavaScript での modal view の表示

## 第2回　ハイブリッドアプリ#2, 開発環境の構築と最初の一歩
* ハイブリッドアプリの概要を知る
* 開発環境の構築
* cordova の利用（Android に実機転送？）

## 第3回　カメラの利用？

# Cordova インストール方法
## 0 事前準備
※別途，Android SDK や Xcode をダウンロードしておくこと
1. Node.js のインストールに関して
Node.js に付属する npm コマンドで Cordova をインストールするが，そのまま入れるとバージョン管理が大変なのでNode.jsのバージョン管理ツールを先にインストールする
2. Mac の場合：nodebrew
  * curl -L git.io/nodebrew | perl - setup
  * export PATH=$HOME/.nodebrew/current/bin:$PATH
3. Windows の場合：nodist
  * nodist からzipダウンロード or git clone git://github.com/marcelklehr/nodist.git
  * nodist のパスの指定（システムの詳細設定から環境変数に「...\\nodist\\bin」を追加。pathの区切りは「;」）
4. それぞれのバージョン管理システムが正しく作動しているか確認
  * nodebrew
  * nodist -v

## 1 Node.js のインストール
1. バージョン管理システムそのもののアップデート
  * nodebrew selfupdate
  * nodist update
2. バージョン管理システムを使用し，インストール（今回は最新安定板を使用）
  * nodebrew install stable
  * nodist stable
3. インストールしたNode.jsのバージョンを確認
　* node -v

## 2 Cordova のコマンドラインツールのインストール
1. -g コマンドでグローバル領域にインストール
  * npm install cordova -g
2. Cordova のバージョンチェック
  * cordova -v
3. 念のため cordova コマンドのアップデートを実施
  * npm update cordova -g
4. Android SDKに含まれるディレクトリにpathを通す
  * Mac の場合
    * echo "export PATH=$PATH:...(自分のAndroid SDK のpath).../sdk/tools/" >> ~/.bash_profile
    * echo "export PATH=$PATH:...(自分のAndroid SDK のpath).../sdk/platform-tools/" >> ~/.bash_profile
  * Windows の場合
    * 以下のパスを環境変数に追加
    * ...(自分のAndroid SDK のpath)...\\sdk/tools\\
    * ...(自分のAndroid SDK のpath)...\\sdk\\platform-tools\\
4. android コマンドと adb コマンドの確認
  * android -h
  * adb version

## 3 Cordova コマンドの使用
1. プロジェクトの作成
  * cordova create [ディレクトリ名] [アプリ識別子] [アプリ名] -d
  * -dオプションはcordova コマンドの途中経過を表示するオプション
2. プラットフォームの追加
  * cordova platform add ios
  * cordova platform add android
  * 現在の登録されているプラットフォームの確認
    * cordova platform ls
  * 登録済みのプラットフォームの解除
    * cordova platform remove ios
3. ios シミュレーター，Android エミュレータの使用
  * Android エミュレータの使用  
    * cordova emulate android -d
    * Android SDK で足りないAPIがある場合
      * 管理者権限のある状態で，android コマンドを実行し，足りない API を追加
  * ios シミュレータの使用（ツールをインストールする必要あり）※Macのみ
    * Homebrew のインストール
      * ruby -e "$(curl -fsSL https://raw.github.com/mxcl/homebrew/go)"
    * Homebrew から ios-sim をインストール
      * brew install ios-sim
    * ios シミュレータの起動
      * cordova emulate ios -d
4. 実機転送(コマンドからの利用は Android のみ)
  * cordova run android -d
  * ios の場合は，platform/ios 以下の「.xcodeproj」ファイルを指定すると自動的にXcodeで開かれる。実行は Swift や Objective-C の場合と同じ
    * open platform/ios/アプリ名.xcodeproj
5. 実機転送ができない場合（Windoiws / Android）
  * デバイスのUSBデバッグを可能にする
    * Android 5.0 Lollipop では設定の端末情報にあるタブレット情報をタップし，ビルド番号の欄を連打します（約7回）。開発者向けオプションが表示されるようになると，メッセージが表示される
    * 開発者向けオプションの中から USB デバッグを許可する 
    * この時点で解決されない場合は，以下の項目に進む
  * デバイスを認識しているかの確認（エクスプローラ上に表示されていても，デバイスが認識されているわけではない点に注意）
  * 接続されているデバイスの確認
    * adb devices
  * リストに何も表示されなければ，デバイスマネージャを表示
  * 実機の名前に黄色い警告マークがついている場合，対象のデバイスが認識されていない
  * SDKマネージャーの起動
    * android
  * Extra >  Google USB Driver のインストール
    * この際にpathの確認をし，コピーしておく
    * もし，実機の Android のバージョンのAPIがインストールされていなければ，一緒にインストールしておく
  * デバイスマネージャから対象のデバイス選択（右クリック）しドライバーソフトウェアの更新を選択
  * 参照から，コピーしたパスを指定しインストール

## デバッグに関して
* Google Chrome の拡張機能，ADB を使用
* Chrome のデベロッパーツールと同等の環境でデバッグできます。このあたりの使い方はWebの授業で培ったノウハウでカバーしましょう。このあたりがハイブリッドアプリの学習コストの低さの一つでもああります
* Chrome Webストア から検索して Chrome に追加
* アプリケーションの実行後に，拡張機能を起動して起動しているアプリケーションを選択
