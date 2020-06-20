## 目的
Open Sourceにはどのような技術が使われ、どのように構成されているかを知る。
コードリーディングというのはどのような感じかを知る。




## 概要
対象プロジェクト：http://github.com/sindresorhus/emoj

言語：node.js

選択した理由

1. フォルダ階層が浅いため（depth=1）、読みやすそう。
2.  スターが2kを超えの評価がされているため、信頼度高め。
3. JavaScriptのため、読みやすそう。
4.  sindersourhus氏、nodeの世界では有名人らしい。




### ディレクトリ構造
> emoj/  
> 　├ .github/ (githubの設定ファイルを格納)  
> 　│　└ funding.yml （sponserdの設定ファイル）  
> 　├ **.editorconfig (editorの設定ファイル)**  
> 　├ .gitattributes (gitの設定ファイル)   
> 　├ **.gitignore (gitの無視設定をおこなうファイル)**  
> 　├ .npmrc (npmの設定ファイル)  
> 　├ **.travis.yml (TravisCIの設定ファイル)**  
> 　├ cli.js    
> 　├ index.js   
> 　├ **LICEENSE (ライセンス)**  
> 　├ **package.json**  
> 　├ **readme.md**  
> 　├ **test.js （テスト）**  
> 　└ ui.js    
>
> ※ 太字はexpressjsにも含まれていた（名称は異なる）もの 
* スクリプト本体とpackage.jsonのほかに以下のものは**必須**のようだ 
	* エディタの設定ファイル (.editorconfig) 
	* gitの無視設定ファイル (.gitignore) 
	* CIの設定ファイル (travis.yml)
	* ライセンスを記述したファイル (LICENSE) 
	* テストプログラム (test.js) 
	* 概要の説明 (readme.md)
* emojではプロジェクト直下にjsファイルを格納しているが、一般的にはindex.js以外は/libの下に格納する(ex. expressjs)


### 各ファイルの気になる点
**readme.md**

概要、インストール方法(Install)、 使い方(Usage)、 関連(Related)の構成

**package.json**

　`main`がなく`bin`を使用している。

　`bin`に記載することで、インストール時に`./node_modules/.bin`に実行可能ファイルのシンボリックリンクを張り、設定したコマンドでスクリプトを実行できる。（ローカルインストールの場合）

下記のpackage.jsonの場合

```json
{  
    "name": "emoj",	
    "bin": "cli.js"
}
```
このコマンドが使えるようになる
```bash
$ emoj
```

そのほか
`engines`：Node.jsのバージョンを指定できる。実行環境のバージョンを固定したいときに便利。
`keywords`：パッケージマネージャーで検索するために設定するキーワード
`files`：パッケージに含まれるファイルを記述
また、`xo ava`というものを使っていることがわかる。

**xo**：sinderesorhus氏の考えるESLintの設定でLintする（内部でLintを使用している）
**ava**：テストランナー

※ どちらもsindresorhus氏が作成したもの




### プログラム概要

**cli.js**

entryポイント

使用モジュール

​	meow : cliコマンド作成ツール

　react, import-jsx, ink : React系

　clipboardy：クリップボードにアクセス

　skin-tone：絵文字の色を変える

　conf：configのset, get

**index.js**

　サーバへアクセスしたりなど処理の中心。

**ui.js**

　絵文字を選択したりするUI



## 所感

コード数は少ないが、Reactの知識が必要のため読みこなせなかった。

