# これは何？

RubyLive という Debian GNU/Linux ベースの LiveCD を作るために使用する live-build の
設定ファイル集です。Debian の wheezy を利用しています。

- [live](http://live.debian.net/)

## どうやって使うの？

    $ rake -T

コンソールで上記のコマンドを実行すると出来ることの一覧を表示します。

## RubyLive でのカスタマイズポイント

- 壁紙の変更
  - RubyKaigi 2014 のロゴを使用している
  - http://rubykaigi.org/2014
  - This work by RubyKaigi 2014 Team is licensed under a Creative Commons Attribution 3.0 Unported License.
- デスクトップにワークショップで使用するアイコンが置いてある
- デスクトップに[Rubyリファレンスマニュアル chm版リミックス](http://ruby.morphball.net/refm-remix.html)が置いてある

## カスタマイズしたい

auto/{build,clean,config} を書き換えると基本的な部分をカスタマイズできます。
RubyLive に必要なことは書いてあるので変更する必要はあまりないでしょう。

- config/binary_grub/
  - ブートローダのスプラッシュ画像を置くディレクトリ。
- config/hooks/
  - インストールの最後の方で実行するフックスクリプトを置くディレクトリ。
  - 拡張子を .chroot にして実行権限を付けておく。
- config/includes.chroot/
  - このディレクトリを root に見立てて LiveCD 環境にコピーしたいファイルを置くディレクトリ。
- config/package-lists/
  - 特別にインストールしたいパッケージのリストを置くディレクトリ。
  - 拡張子を .list.chroot にしてパッケージ名を列挙する。

## テストするには

[VirtualBox](http://www.virtualbox.org/) や qemu などの仮想化環境を使うと便利です。
