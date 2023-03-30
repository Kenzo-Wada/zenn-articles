---
title: "vercelでブランチ単位で差分を見て、特定のディレクトリのみbuildさせる"
emoji: "🚀"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ['vercel', 'git']
published: true
---

# is何

この記事では、vercelでignore build stepを用いて特定のディレクトリでの作業の時だけビルドされるようにする手順を公開しています。
具体的には、vercel公式の手法だと**直近のコミットとその1つ前のコミットの差分しか見ていない**ため、それらのcommitで作業ディレクトリ外の作業をしてしまうとビルドがcancelされてしまいます。
そこで、コミット単位ではなく**ブランチ単位で差分を見てignore buildさせる**方法を提案します。

# 前置き

例として、この記事では以下のようなディレクトリ構成を想定して説明します。

```bash
root //vercelにおけるroot directory
  └client
  └server
```

# [vercel公式の手法](https://vercel.com/guides/how-do-i-use-the-ignored-build-step-field-on-vercel#with-folders-and-workspaces)

たとえば`client`配下のみbuildさせたい時、公式のドキュメントではignore build stepに下記のような記述をする方法が提案されています。

```bash
git diff HEAD^ HEAD --quiet ./client
```

しかしこの方法では、直近のコミットとそのひとつ前のコミットの差分しか見ていないため、ずっとclient配下で作業していたとしても、「server側も修正しちゃお。」と急に思い立って2回server配下のみの修正をpushしてしまうと、ビルドがキャンセルされてしまいます。

# ブランチ単位でgit diffする

参考文献：[probablyup/script.sh](https://gist.github.com/probablyup/cf7cbec809f1695f91e0fb5ce8cd0f9b)

結論から書くと、このようなコマンドとなりました。

```bash
git remote add -f origin https://$GITHUB_ACCESSTOKEN@github.com/{githubのrepository名}
git diff --quiet origin/develop origin/$VERCEL_GIT_COMMIT_REF -- ./client
```

当初の想定ではgit diffでdevelopと作業ブランチを単純に比較すれば良いと思っていたので、下記コマンドのみ叩こうとしていました。

```bash
git diff --quiet origin/develop origin/$VERCEL_GIT_COMMIT_REF -- ./client
```

しかし、vercelがgit cloneする際にdepth=2を指定しているという落とし穴があり、うまくいかず。最終的には参考文献を参考に、git remote addを用いてブランチを読み込ませてあげることでやりたかったことができました。

# 最後に
Next13でturbopackが発表されたりなど、昨今ではvercel社によるエコシステムが巨大化しているように感じています。この流れに乗って、vercelを使いこなしていきたいです！その一歩として、どなたかの参考になれば幸いです！

