# Run

- 実行にはJava 8以降の動作環境を推奨します．（それ以下では未テスト）  
- コマンドライン上で適宜引数を与えて実行します．  
   - （例）`java -jar CCFinderSW.jar -d directory -l language -o outputtxt`  
- CCFSWで出力されたクローンペア情報は，GeminiまたはCCFXで読むことができます．

## コマンドラインの引数  

### 必須の引数
- -d <arg>
   - ソースファイルがあるディレクトリパスを入力します．  
- -l <arg>
   - コードクローン検出の対象となる言語名を入力します．  
   - オプションファイルを読み込む際に，この言語名を使用します．
- -o <arg>
   - クローンペア情報を出力したいファイル名を入力します．  
   例 `-o outputfile` と入力すると *outputfile.txt* が作成される．
   - ccfxモードなら *outputfile.ccfxd*が作成される．
   - ccfswモードなら *outputfile_ccfsw.txt*も作成される．

### 任意引数
- -t <arg>
   - 検出するコードクローンの最低トークン数（しきい値）を入力します．  
   例 `-t 90`のように数値を入力してください．
   - 参考：CCFinderの最低トークン数の約1.8倍程度を入力すると，近い設定となることが多いです．
   - デフォルトは50です．引数を与えなければデフォルト値になります．
- -ccfx  
   - ccfxモードで実行します．  
   - 引数を与えなければgeminiモードで出力します．  
   - ccfxと同じ出力形式のccfxdファイルとccfxprepファイルが作成されます．
- -ccfsw <arg>  
   - geminiモードまたはccfxモードに加え，CCFSWの出力形式でも出力します．  
   - ファイル名の最後は *_ccfsw.txt* が付きます．
- -charset <arg>   
   - 対象ファイルの文字コードを選択しています．
   - 全角文字などが使用されたソースコードの解析は，正しく文字コードを認識する必要があります．
   - sjis, utf8, euc, auto の4種類があり `-charset sjis` のように入力します．  
   *sjis* 文字コード「Shift-JIS」で全ファイルを認識します．  
   *utf8* 文字コード「UTF-8」で全ファイルを認識します．  
   *euc*  文字コード「EUC-JP」で全ファイルを認識します．  
   *auto* はファイル毎に，上記三種類の文字コードから自動認識を行います．処理に少し時間がかかります．  

### 引数なし，もしくはエラーのある引数での実行
-  引数なし，もしくはエラーのある引数での実行でusageが出力されます．

## 対象ソースコードについて
- 検出したいソースコード全てをあるディレクトリに入れ，そのディレクトリのパスを前述の引数で設定すればOKです．

- CCFXモードを使用すると，ディレクトリ内に「.ccfxprep」というフォルダが作成されます．これはCCFXのViewerを使用するときに必要です．

## 実行のための準備・条件

- 実行には，言語対応のコメントファイルと予約語ファイルが必要です．
   - コメントファイル
      - **最低限の記述が必要です．** 詳しくは[Option.md](/UsageJp/Option.md)で説明されます．

   - 予約語ファイル
      - 必須ではありませんが，置くことを推奨します．
      - ファイルが存在するとタイプ2までのコードクローンを検出し，そうでなければタイプ1のコードクローンを検出します．

- ファイルの置き場所
	- コメントファイルと予約語ファイルはcommentディレクトリ，reservedディレクトリにそれぞれ置いてください．