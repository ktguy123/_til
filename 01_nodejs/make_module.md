## 1. 概要

1. Node.jsのモジュール作成における基本的なディレクトリ構造について
1. `export`, `require`について
1. assertモジュールを用いたテストの記述方法について
1. モジュールをnpmレジストリにアップロードする手順



TODO：モジュールのリファクタリングについて

TODO：モジュールの拡張について



## 2. 参考資料

Nodeクックブック 9章 (O’REILLY)



## 3. 本文

### 3-1. ディレクトリ構造

以下の通り

> module_name/   
> 　├ lib/  
> 　│　└ [index].js  
> 　├ test/  
> 　│　└ [index].js  
> 　├ examples/  
> 　└ index.js  

| ファイル、ディレクトリ名 | 内容                                                         |
| ------------------------ | ------------------------------------------------------------ |
| lib/                     | モジュールのスクリプトの本体を記述する                       |
| test/                    | テストスクリプトを記述する。                                 |
| examples/                | モジュールの簡単な使用例をユーザに提供する。                 |
| index.js                 | lib/[index].jsを呼び出す。エントリーポイント。<br>※[index]は任意の名前（モジュール名が一般的？） |



### 3-2. exports → require

呼び出し元 (coller.js)

```javascript
// 複数exportしたい場合
exports.obj = {aa:"aaa"}
exports.coller = function() {...}

// ファイル内の一つの関数を単一モジュールとして公開したい場合
// module.exports = function(){...}
```

呼び出し先 (collee.js)

```javascript
const collee = require('coller');

collee.obj;
collee.coller();
```

### 3-3. テストスクリプトいろいろ

```js
const assert = require('assert');
const module_name = require('../index.js'); // テスト対象はmoduleディレクトリ直下のindex.js

// actualがfalsy(false, undefined, null, 0, NaN, "")ならエラー
assert(actual, 'error message'); 
// errが発生したらエラー
assert.ifError(err);
// actual == expected なら正常
assert.equal(actual, expected, 'error message');
// actual !== expected なら正常
assert.notStrictEqual(actual, expected, 'error message');
// 最後に記載
console.log('all ok!');
```

 

### 3-4. アップロード手順

1. `package.json`を作成する。（`npm init`）

   name : 必須。nameで指定した値をrequireに渡すことでモジュールを呼び出すことができる。

   version : 必須。 `メジャー.マイナー.バッチ番号-[ビルド番号]`で構成 。

   main : mainプロパティに指定したパスがentryポイントになる。

   scripts : npm runで実行できるコマンド一覧。

2. npmアカウントを作成

   `npm adduser`

3. npm publish
