---
title: "【2024初頭】新規開発で使ってみたいモダンフロントエンド最前線"
emoji: "💮"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["next", "bun", "turborepo", "biome", "mantine"]
published: false
publication_name: ficilcom
---

## TL;DR

弊社で実験的に導入を始めている、2024初頭時点で今後に期待が高まる最新のweb技術についてまとめています。
新規プロダクトの技術選定に迷っている方などにおすすめです。

## [Turborepo](https://turbo.build/repo) - Monorepo管理

モノレポ構成における懸念点の一つとして、プロダクトが大きくなるにつれてビルド時間が膨大になって来る点です。
TurborepoはRust製、並列化、差分ビルド、Remote Cashingなど、肥大化しがちなmonorepoのビルド時間を短縮するメソッドがたくさん詰まっています。

https://turbo.build/repo

## [Bun](https://bun.sh/) - Package manager (runtime, test tool)

正確にはBunはランタイムですが、Nextなど厳密にはNode.jsで動かす必要があるため、弊社では（ほぼ）パッケージマネジャーとして活用しています。
pnpmやyarnと比較してnpm installなどの時間が短縮され、開発体験が向上しました。
また、Denoとは違い、Node.jsと同じくpackage.jsonを見てパッケージ管理をするのでNodejsからBunの移行もとても簡単に行えます。
さらには、[bun:test](https://bun.sh/docs/cli/test)というテストツールも提供しており、こちらはVitestよりも実行速度が早いです。
前述したとおり、またエコシステムが整っておらず少なからずNodeと併用する形にはなりそうですが、今後に期待です。

https://bun.sh/

## [proto](https://moonrepo.dev/proto) - Version Manager

Node.jsのバージョン管理ツールとしてはVoltaやnodenvなどがありますが、bunのバージョン管理ツールとしてはprotoがあります。
Protoはbunのバージョン管理ツールと言うわけではなく、様々なToolのバージョン管理ができるので、筆者は思い切って諸々の管理をProtoへ移行しました！
repositoryに.prototoolsというファイルを作成することで、チーム内でバージョンを管理することができます。
まだv0のため、v1リリースに期待です。

https://moonrepo.dev/proto

## [Biome](https://biomejs.dev/ja/) - formatter, linter

Rust製のformatter, linterです。2024のロードマップによると、今後はCSSの対応を最優先で行うと書いており、将来的にはeslint, prettierだけでなくstylelintの代替としても期待できそうです。

https://biomejs.dev/ja/

## [Mantine]() - UI library

Next.jsを用いて開発する際、emotionなどのCSS-in-JS依存なUIライブラリとRSCの相性が悪く悩みがちです。
とはいえ、RadixのようなヘッドレスなUIライブラリはいちいち自前のcssを当てるのが面倒くさいという悩みも...。
そこでおすすめするMantineは、豊富なコンポーネントを提供してくれている、CSS ModulesベースのUIライブラリです。
Mantine v6以前はemotion依存でしたが、v7でCSS Modulesへ置き換わり、RSCとの相性がよくなりました。
現在は、Rechartsをwrapした@mantine/chartsというChartライブラリも絶賛実装中のようで、より一層使いみちの幅が広がりそうです。
筆者もときどきcommitしたりissueをあげており、おすすめのライブラリの一つになります！

https://mantine.dev/

## [v0]() = UIデザイン

プロンプトからUIでざいんをさ作成してくれるサービスです。
ただ画面を作るだけでなく、コードも出力してくれるのもとても便利。
文字によるプロンプトだけでなく、画像からUIも作成してくれる機能もあるので、筆者は手書きのワイヤーフレームを読み込ませてデザインの清書に活用しています！

https://v0.dev/


## 最後に

2023年は数多くの新しい技術が出てきており、2024年にもとても期待が高まります。
ここで紹介した技術は、まだ日が浅いこともあり未知のバグが数多く存在します。
ぜひ、活用しながらバグを見つけたらIssueを起票してあげて、より今後の発展にみなさんで貢献していきましょう！
