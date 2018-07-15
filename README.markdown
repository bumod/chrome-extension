# はてなブックマーク Google Chrome 拡張

## オリジナルからの変更点

- ブックマーク数が0ならバッジを表示しない [#20](https://github.com/bumod/chrome-extension/issues/20)
- フラット風のUI [#19](https://github.com/bumod/chrome-extension/issues/19)
- Tab キーでナビゲートできる [#16](https://github.com/bumod/chrome-extension/issues/16)
- Twitter の URL へのブックマークに関する不具合をパッチ [#11](https://github.com/bumod/chrome-extension/issues/11)
- HTTPS のページでもブックマークカウンターを表示できる（設定でオプトイン）[#7](https://github.com/bumod/chrome-extension/issues/7)
- 他の人のコメントのタグを表示できる from [@dlwr](https://github.com/dlwr)  [#9](https://github.com/bumod/chrome-extension/pull/9)
- 自分がつけたスターを削除できる（約5秒マウスカーソルを重ねて）
- 高精細（Retina）ディスプレイ対応 [#5](https://github.com/bumod/chrome-extension/issues/5)
- 不要な権限を除去 [#8](https://github.com/bumod/chrome-extension/issues/8)
- Google Analytics を除去 [#6](https://github.com/bumod/chrome-extension/issues/6)
- エンドユーザーライセンス契約を削除 [#4](https://github.com/bumod/chrome-extension/issues/4)
- 名称変更 [#4](https://github.com/bumod/chrome-extension/issues/4)

## インストール方法

- [ダウンロード](https://github.com/bumod/chrome-extension/releases/latest)
- [インストール方法](https://github.com/bumod/chrome-extension/wiki/%E3%82%A4%E3%83%B3%E3%82%B9%E3%83%88%E3%83%BC%E3%83%AB%E6%96%B9%E6%B3%95)

---

＊以下、オリジナルの README。

---

本文書は, はてなブックマーク Google Chrome 拡張の開発者向けです。
利用者向け情報は下記ページなどをご覧ください。

* http://b.hatena.ne.jp/guide/chrome_extentions

## ブランチの使い方

永続的なブランチとして下記の 2 つを使用しています。

* master
* dev

開発時は dev ブランチから新しいトピックブランチをきって、トピックブランチでの開発が終了した時に
dev ブランチにマージ (または pull reqeust) してください。
本番リリースの際には dev ブランチを master ブランチにマージしてリリースします。

## テストについて

src/tests にテストがあります。
テストは, はてなブックマーク Google Chrome 拡張をインストールしている Chrome で
chrome-extension://{extension-id}/tests/test.html にアクセスすると実行されます。

## パッケージングについて

リリースのための zip ファイルには src/tests を含める必要はありません。
(`rake package` により ZIP ファイルを作成すると自動的に src/tests 以下は除かれます。)
```
rake package
```

## ソースファイルの配置

Chrome 拡張と Opera 拡張を同じブランチで管理できるように、ソースファイルの配置は少し複雑になっています。

* src/main ディレクトリ: どの製品向けのパッケージにも含まれる基本的なソースファイル
* src/chrome ディレクトリ: Chrome 用のパッケージに含まれるファイル
* src/opera ディレクトリ: Opera 用のパッケージに含まれるファイル

複数ファイルに分散しているため、このままだと開発用に Chrome や Opera で読み込むことができません。
そこで、これらのソースファイルをコピーして、obj/* ディレクトリ以下に配置するための Rake タスク filecopy が存在します。

```
bundle exec rake filecopy
```

また、ソースファイルの変更時に自動的に filecopy タスクを実行するための watchr 設定ファイルもあります。

```
bundle exec watchr filecopy.watchr
```

## Ruby Gems の管理

`rake` や `watchr` に必要な Ruby gems は bundler で管理しています。

* [Bundler: The best way to manage a Ruby application's gems](http://gembundler.com/)
* [bundle install 周りのドキュメント](http://gembundler.com/v1.3/man/bundle-install.1.html)

Bundler がインストールされている状態で次のコマンドを実行すると、このプロジェクトで必要な Gem がインストールされます。

```
bundle install
```
