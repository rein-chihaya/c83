# Gitの特徴

## 分散型

gitは分散リポジトリ型です。
分散型にはsvnのような中央リポジトリはなく、
リポジトリの完全な機能は個々のコンピュータにあります。
以降、個々のコンピュータの中にあるリポジトリのことを **ローカルリポジトリ** と呼びます。

しかし、普通はプロジェクトの成果を共有する必要があるので、
中央リポジトリと同じような立場の **共有リポジトリ** を用意するケースがほとんどだと思います。
共有リポジトリは自分でサーバを立てたり、githubに持ったりするでしょう。

その場合でも、共有リポジトリはただ共有するためでしかなく、
コミットなどの作業はやはりローカルのリポジトリへ行うことになります。

## 分散型のメリット

分散型リポジトリでは、ローカルリポジトリへの操作で、共有リポジトリが変更されることはありません。
そのため、

- ネットワークにつながっていなくてもリポジトリ操作ができる
- ネットワークを介さないので基本的な操作が速い
- ローカルで完結するのでコミットがしやすい
  - ブランチが圧倒的に使いやすい
  - ブランチの切り替えがしやすく、つまり作業の切り替えがしやすい
- 操作のやり直しや歴史改変ができる

というメリットがあります。

## 分散型で注意すること

共有リポジトリが変更されないという事は、明示的に共有の操作をする必要があるという事です。
多くの場合、共有リポジトリとローカルリポジトリには乖離が発生し、共有操作で少しずつ解消されていきます。
gitでは、この共有操作が一番難しく、これを完全にコントロールすることが重要です。

共有されているコードとされてないコードの区別を常に意識し、
まだ共有されてはいけないコードが共有されないようにする必要があります。