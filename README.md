# Word Corpus Generator for Fingerspelling Recognition
指文字認識のための単語コーバス生成器

## Requirements  
- pandas
- jaconv (ひらがな・カタカナ・全角・半角の変換)
- pykakasi (漢字 -> ひらがなの変換)
- requests
- more_itertools

## Method
1. 下のリストから、ひらがな10文字に収まる日本語を収集する
   - [郵便番号データダウンロード - 日本郵便](https://www.post.japanpost.jp/zipcode/download.html) (`読み仮名データの促音・拗音を小書きで表記するもの`をDLする。Shift-JIS形式なので扱いに注意。)  
   - [日本語能力試験出題基準語彙表](http://www7a.biglobe.ne.jp/nifongo/data/index.html) (`日本語能力試験出題基準語彙表(TSVファイル)`をDLする。TSV形式なので扱いに注意 。)  
   - [カタカナ語の認知率・理解率・使用率【使用率順】 | 文化庁](https://www.bunka.go.jp/tokei_hakusho_shuppan/tokeichosa/kokugo_yoronchosa/h14/katakana_shiyo.html) (表をコピペしてTSV形式で読み込み。)  
   - [openBD](https://openbd.jp/) (APIを使用して日本の本のタイトルを取得。)  

2. 正規表現`[あ-んー]`を`L`と定めた時、`L`の二つ組`LL`を基本として考え、(1)で収集した日本語リストから    
   1. 一度しか登場しない`LL`を含む単語を全て採用する  
   2. 新しい`LL`を最も多く含む単語を採用する  
   3. (ii)を未出現`LL`がなくなるまで繰り返す  
3. 採用された日本語リストを指文字認識のためのコーバスとする

## Reference  
- 江本 祐太, 宮島 千代美, 伊藤 克亘. HMMに基づく連続指文字認識・合成用コーパスの構築. 電子情報通信学会技術研究報告 = IEICE technical report : 信学技報. 2005, vol.105 , no.295, p.53-58. （コーパスの構築に参考させて頂きました）  
- [ryuuji/openbd-downloader](https://github.com/ryuuji/openbd-downloader) (openBDから全ての日本書籍タイトル取得の参考にさせて頂きました)  

## Author  
Redgum(https://twitter.com/redgum775)  

## LICENSE  
[MIT License](LICENSE)