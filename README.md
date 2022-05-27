# 秀丸へのmarkdownモード用のプラグインの提案  

### 前置き  

現行、何かサイトー企画さんの方で秀丸エディタに対して集中して取り込んでいる大きな機能があるなら  
そちらを優先していただきたいですが、  
「とりたててそういった大きな優先実装事項は存在しない」  
「ユーザーに指摘された細かなバグや機能改善のみ」ということであれば、  
大きなコンポーネントとなりますが、markdownモードを作ってみてはいかがですか程度の提案です。  

「作ってみてはどうでしょう？」などと言いっぱなしもなんなので、  
思いつくままアイデアっぽい何かを添えてみます。  

### テクニカル系ではない人をターゲットに据える  

技術畑の人用のマークダウン支援というよりは  
技術解説文用というよりは、「普通の文章用」あるいは「メモ用」といった方向にフォーカスを合わせる  
まだマークダウンをあまり使っていない人が、秀丸で日本語文章を書く行為の延長で、  
自然とマークダウンを取り扱えるのがベスト。  

### 秀丸は「日本語文章入力」においては依然人気あり  

MarkdownはHTMLとは異なり「浅い段落とリスト項目を使った文章」「テーブルあり」「画像・バッジ画像」程度ものが大半です。  
日本語文章入力においては秀丸はVSCodeより選択されやすいわけだから、やりようによっては注目され、多くのユーザーに使ってもらえる機能となるかと思います。  
(但し現行すでにMarkdownをVSCodeで利用しているユーザーには訴求しにくい)  

### VSCodeとの差別化、VSCodeの弱点  

私自身が6年くらいVSCode 1.0の頃から使っているので逆によくわかるんですが  
VSCodeは キーバインドショートカット と コマンドパレット での操作に集約されているため  
技術畑はない人がこの操作でMarkdownを入力していくのは敷居が高いハズです。  
(実際にやってみればどうということはないのですが、IT系と遠い人ほど  
 VSCodeの有り様はそれ自体が敷居が高いと思う人が多いかと)  

Markdownのタグを支援するようなボタンを用意すれば大きく緩和できますが、  
VSCodeを利用する層と噛み合わないため、当面はデフォルトでは実装されないでしょう。  

### マークダウンはWYSIWYGをブレンドした独自仕様へと細分化している  
以前はマークダウンにテキスト入力のみで対応していたSAASやブログが、    
最近ではWYSIWYGとテキストの両方のモード搭載、あるいはハイブリッド入力方式になってきていることからも    
技術畑はない人々にまでMarkdownの使用の裾野を広げるには、    
「テキストタグのみでの入力」では限界があったことがわかります。    

### いつかMarkdownは廃れてなくなる  

10年程度は全然大丈夫でしょうが、20年後は無いかも...    

マークダウンは時代を経る中で廃れて別の形態へと変化していく可能性も高い。    
本体に入れるのではなくプラグイン扱いにしたほうがいいと思われる。    
(思ってるよりも早く誰も使わなくなった場合に、最悪は取り下げられる)  

マークダウン機能は、レンダリングにおいて外部コンポーネント依存せざるを得ないかもしれません。  
(WZ Editor などは独自のレンダリングをしているようですが... 違和感大)  

## 制作の方向性の提案  

## 基本的な画面構成スタイル  

左テキスト・右プレビュー・上部にメニューボタン・テキスト選択時のみ出現するパネルボタンあり  
(プレビューは出す出さない自由）  

## 機能など  

- 基本的なところではVSCodeに「Markdown all in one」の拡張機能と「Paste Image」を入れたような挙動。  

- 「VSCodeでは突き放して捨てて」しまっている「非技術畑の人に寄り添う機能」を付けていく  
- 「Markdownタグボタン」を秀丸の上部メニューに並べたり、  
- テキストを選択すると近くにそのシチュエーションでよく利用されるボタンのパネルが出るなど  
    -  Milkdown参照。  

## 参考になるエディタやサービス  
- VSCode + Markdown All in One  
- GithubのPull Requestの画面(絞り込んだボタン)  
- Typora(マークダウンにはどのような機能があるのかメニューからわかる。  
　WYSIWYGとテキスト入力とを融合するとこうなるというのもわかるがこの実装は敷居が高い)  
- Milkdownの画面(絞り込んだボタン)  
    - 各種Markdownが使えるようなSaaSやWordPressのマークダウン系プラグインなども上記４つのいずれかと類似します)  

## 風呂敷ひろげすぎかなと思う機能  
- (Typoraのような)テキストで入力すると即座にWYSIWIGになる、「テキストのタグの入力エリア＝レンダリングエリア」みたいなことは  
　めちゃくちゃ実装コスト大きいうえ、テキストエディタの領分ではないかもしれません。    
　このため、左はテキスト、右はライブビュー といった一般的な形でよいかと。  


## 実装するならこれは必須と思われる機能  

- 右にビューワー。編集エリアと同期する。    
- ビューワーの方をスクロールするとテキストエリアが合わせて移動、  
  逆に、テキストエリアをスクロールすると、右のビューワーが合わせて移動  
  「スクロールの同期の痙攣減少」が起きやすいので注意(VSCodeのプラグインでも起きている)  
- テキストエリアで「今、編集している位置」に、右のライブビューの「見えてる位置」は追従するようにする（必須）  
- リスト項目の文章を入力している際、改行すると次のリスト項目となる（ほぼ必須） (VSCodeのMarkdown All In Oneを入れると体験できる)  
- リストが「番号型」なら、「間にリスト項目」をはさむと番号が自動的に再整理される。 (VSCodeのMarkdown All In Oneを入れると体験できる)  
- Github Flavored Markdown の範囲は対応。    
特にテーブルが使えない(いわゆるただのノーマルな)Markdownだと使いみちがかなり限定されてしまう。(テーブルだけは必須)  
- 直近のクリップボードがhttpプロトコルであった場合、テキストを選択しつつCTRL+Vを押すと、選択したテキストを対象のhttpプロトコルでリンクを貼る  
- 画像のコピー＆ペーストに対応する。  
  - 「クリップボードが画像イメージ」ペーストするとその場で画像タグを作成しそこに画像Markdown挿入。(VSCodeの「Image Paste」相当)  
  - 直近のクリップボードが画像イメージかもしくは画像ファイルなら、CTRL+Vで自動的にイメージタグとなる。  
  -「クリップボードが画像イメージではなく、画像ファイル」なら相対ディレクトリにできそうな範囲なら相対URL、そうでないなら絶対URLにして画像Markdown挿入。（これはほとんどのMarkdownエディタがやっていない）  
  -「画像ファイルを編集テキストエリアの該当行へとドラッグ＆ドラップ」→ここまでできれば理想的。  

- テーブルのプロトタイプボタン、テーブルのテーブルテンプレート出力ボタン  
  - ３列＊３行くらいのテーブルテンプレートを出力する方がいいかも。  
- テーブルの整形フォーマット。マークダウンのテーブルはテキストで見ると横幅がガタガタになる。これを整形する。⇒ (VSCodeの「Table Formatter」相当)  
　　Markdownはレンダリング結果だけではなく、テキスト側を見ても文章やテーブルとしてわかりやすいことが求められるため。  
　　(すでにテーブルMarkdownになっている範囲を選択して整形するのが良い。）  

- CSSの外部適用。各要素をどのようにレンダリングするかカスタム出来ると理想    
  - なくてもいいですが、その時はGithubのMarkdownからのレンダリング用CSSに近い見た目の方が違和感が少ないです。  
    - GithubのMarkdownのCSSに近い見た目。  
    - https://github.com/sindresorhus/github-markdown-css/blob/main/github-markdown-light.css  
    - https://github.com/sindresorhus/github-markdown-css/blob/main/github-markdown-dark.css  
　　　　　　　（一般的にはdarkではなくlightが標準とされている)  
- テキスト選択中に頻繁に使う機能は、選択中のテキストに近い距離に別途ボタンを出す。（→Milkdowでテキスト選択してみると参考と表示がみられる)  
- 外部ブラウザで(HTMLになったものを)見る機能。単一HTML化(持ち運びや簡単にブラウザで取り扱えるように)  
- 「PDF化」「eBook化(ePub, mobi, PDF HTML)」  
-  ツリー  
   - Markdown Navigation  
   - 秀丸のアウトラインの正規表現で賄える範囲かも  

### 迷う機能  

- 数式対応やUML等々は要望はすくないかも。  
	- VSCode Markdown Math  
  - 単発で数式やUMLだけ対応されていても意味がうすく、統合的な環境を要するため、数式系との相性が良いVSCodeに移住済みが大半なはず、あるいはLatexユーザー。  

- MarkdownLint機能自体はあったほうが良いと思うが、常時適応だとうっとうしいかもしれない  
　　そんなキッチリしたLintに叶うMarkdownってあまり書かないし、Lintに従うと行が隙間だらけに  

---  

# 以下は備考  

## 秀丸の機能とマークダウンエディタ  


## Markdownエディタとしての基礎コンポーネント  

### 秀丸は分轄表示を備えている  

左をマークダウン編集エリア、右をプレビューエリアなどにする下地がある。  
この入力スタイルはマークダウンエディタではやや古風ですがオーソドックス。  

### 秀丸にはファイルマネージャがある  

同じフォルダ内の別のマークダウンファイルをすぐに選択できる下地があり便利に機能する。  

### 秀丸メールではプラグインではあるものの、WebView2での実績があります  

HTMLをレンダリング出来るプラグインを作れる下地がある。  
ただし、WebView2にしろ10年といったスパンでは動作しないだろうから、差し替えは覚悟の必要がある。  
秀丸メールでプラグインのHTMLレンダリングエンジンとしてのWebView2を差し替えるタイミングで  
同じように差し替えればよいかも。  

---  

# 以下は懸念  

## 秀丸はGithubに直接対応していない  

正直Markdownにおいてはかなりのハンデ。  
公開・非公開にかかわらず、Markdownファイルのアップ先はほぼ Github / Bitbucket なので。  
エディタでGithubに対応していない時点でクラウド関連全体での使用ではかなり大きなハンデを背負っている状態です。  


