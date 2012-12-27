# おまけ: リリース先輩

実は弊社の公式中央リポジトリはSubversionです。
最近ではgithub:enterpriseが導入されましたが、それ以前もチーム単位でGitサーバを運用していた例もありました。
しかし現在でも最終的にコードはSubversionに置かなくてはいけません。

でももちろん、いまさら馬鹿正直にSubversionなんか使いたくありません。
git-svnも使ってみたけど混乱が増すだけです。

## スクリプト化

### Subversionを自動化

とにかくコミットさえすればいいので、スクリプト化してみました。

- Subversionからtrunkのコードを ./svn に取ってくる
- git archive でmasterをzipでとってきて ./svn に展開する
- ./svn が更新されているのでaddしたりしてcommit

すごく乱暴な方法ですが社内ルールは十分に満たせています。
ポイントは git archive で上書きしているところでしょうか。
Subversionの機能を完全に無視してる感じが最高にクールです。

### リリースwikiを自動化

社内ルールで、リリース内容や作業手順をまとめたwikiページを作らなければなりません。
それを自動化するため、変更内容からwikiページを自動で生成しています。

- git diff で前回とconfigの差分を出す
- git diff で前回のmigrationの差分を出す
- 変更のあるサブプロジェクトを列挙する

さすがに変更内容などは手作業で入力しますが、
コミットメッセージになにかルールづけすれば可能かもしれません。

その他にも、diffを見るtracのurlを生成し、リリースwikiのurlと一緒にチームのIRCチャンネルに送信します。

## 先輩化

リリーススクリプトは誰でも実行できるはずですが、それでも属人性が完全に失われたわけではありませんでした。
日常的にrubyを使っていないと、その実行環境を作ることも難しいのです。
そこで、IRCbotとしてリリーススクリプトを動かすことにしました。
ついでに、通常はストレスがかかるリリース作業が少しでも楽しくなるように、スクリプトを擬人化しました。
それがリリース先輩です。

IRCでリリース先輩に話しかけるとリリース作業してくれます。

```
(masarakki) release_senpai: 先輩お疲れ様です!
(release_senapi) masarakki: おう、おつかれ
(masarakki) release_senpai: 先輩! リリースおねがいします!
(release_senpai) おう、待っとれ

....
(release_senapi) リリースできたぞー
(release_senpai) wikiかけよー http://...
(release_senpai) diffはこっちなー http://...
```

こんな感じです。
リリース先輩のプロセスが死にIRCから退出すると、
「うわっ リリース先輩バックレた!」みたいな悲鳴が上がる楽しい職場になりました。
ちなみにチーム内のヒエラルキーは、jenkins先生が頂点、リリース先輩がその次、人間はそれ以下となっています。