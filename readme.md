# Docker gcc + gdb environment

Docker上でUbuntuのコンテナを作成し、gccとgdbをインストールした環境となっています。

## ディレクトリ構成
```
.
├── compose.yml
├── data
│  ├── dist
│  └── src
│     └── hello.c
├── Dockerfile
├── LICENSE
└── readme.md
```

- [data/](data/): `docker compose` の `Working Directory` となっています
- [data/src/](data/src/): ソースファイル置き場としてお使いください
- [data/dist/](data/dist/): コンパイルしたプログラム置き場としてお使いください([.gitignore](.gitignore)されます)

## 下準備
1. (初回のみ) `docker` と `git`(任意) をインストールし、ターミナルから実行できるようにPATHを通しておく  
- MacOS では [Docker Desktop](https://www.docker.com/products/docker-desktop/)をインストールすることを推奨します。できる人は`homebrew`などを用いてインストールしてください。
- MacOSでのパスの通し方ref: https://zenn.dev/someone7140/articles/a8075a1460f821#path%E8%A8%AD%E5%AE%9A%E3%81%AB%E3%81%A4%E3%81%84%E3%81%A6
2. `cd` でプロジェクトをおいておくのに良さげなディレクトリに移動
3. (初回のみ) リポジトリをclone: `git clone https://github.com/Hikali-47041/docker-ubuntu-c.git`  
`git`をインストールしなかった場合は https://github.com/Hikali-47041/docker-ubuntu-c にアクセスし、Download Zip でリポジトリをダウンロードして解凍。 
4. `docker`のデーモンを起動しておく(Docker Desktopのアプリを起動しておく)
5. `docker compose run ubuntu-gcc gcc -Wall -g3 -o dist/hello.out src/hello.c` でテストプログラムの`hello.c`をコンパイル  
初回実行時は`image: ubuntu:latest`のpull、`apt`のパッケージ更新と`gcc, dgb, vim`のインストール作業が走るので完了までに時間がかかります。
6. `docker compose run ubuntu-gcc ./dist/hello.out` を実行し、 `Hello, World!` が出力されるのを確認

## 使用方法
- `<hogehoge>`: 書き換え箇所(必須)
- `[hogehoge]`: 書き換え箇所(省略可)  
↑ コマンド入力時には `<>, []` の部分を消してください。

### Cプログラムのコンパイルと実行
`docker compose run ubuntu-gcc gcc [-Wall] [-g3] [-o 出力先ファイルパス] <Cのソースファイル名>` でコンパイルできます。

### gdbの実行
`docker compose run -it ubuntu-gcc gdb <デバッグしたいプログラム>` で`gdb`のデバッグコンソールに入れます。

例: 下準備の `hello.out` のデバッグ: `docker compose run -it ubuntu-gcc gdb dist/hello.out`

### Ubuntuのコンテナ内のシェルに入って作業
`docker compose run -it ubuntu-gcc bash` でコンテナ内の `bash` が立ち上がります。  
`bash`のシェル環境から出る場合、`exit` で終了させてください。

## LICENSE
[MIT License](LICENSE)
