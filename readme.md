# Anitime

コンソール上でアニメ等の放送時間情報を表示するPHP製のCLIスクリプトです。
番組データの取得には[しょぼいカレンダー](http://cal.syoboi.jp/)のAPIを使用しています。
実行にはPHP7が必要になります。

## Install

スクリプトファイルの`anitime`をパスが通っている場所にコピーして、実行権限を与えてください。

```
$ git clone https://github.com/tmysz/anitime.git
$ sudo cp ./anitime/anitime /usr/local/bin
$ sudo chmod a+x /usr/local/bin/anitime
```

## Usage

```
$ anitime
```

一度取得した番組データは`/tmp/anitime_{DATE}.json`にキャッシュされ、同日中に再実行した場合は番組データをキャッシュから読み込みます。
`-f`或いは`--force`オプションを使用すると、キャシュを破棄して最新の番組情報を取得します。


## Settings

コマンド実行時に`~/.anitime/config.json`から設定を読み込みます。(設定ファイルがない場合はデフォルト設定で動作します)
`.anitime.example/config.json`に設定例があるので、参考にしてください。

|設定名|形式|デフォルト||
|:--|:--|:--|:--|
|timeStartHi|numeric|2000|表示する放送時間の本日開始時間をHi形式で指定|
|timeEndH|numeric|4|表示する放送時間の翌日終了時間を1~24の範囲で指定|
|ChID|array|なし|チャンネルIDによる絞り込み（[チャンネルID](http://cal.syoboi.jp/mng?Action=ShowChList)）|
|ChGID|array|なし|チャンネルグループIDによる絞り込み（[チャンネルID](http://cal.syoboi.jp/mng?Action=ShowChList)）|
|Cat|array|なし|番組カテゴリIDによる絞り込み（[カテゴリID](https://sites.google.com/site/syobocal/spec/title-cat)）|

- 放送時間が**本日timeStartHi～翌日timeEndH**に含まれる番組が表示されます。
- それぞれの絞り込み配列の中身はORで判断され、異なる絞り込み配列同士はANDで判断されます。

## LICENSE

The Anitime is open-sourced software licensed under the [MIT license](http://opensource.org/licenses/MIT)
