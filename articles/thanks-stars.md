---
title: "OSSにスターをするところから始めませんか？？"
emoji: "🌟"
type: "idea" # tech: 技術記事 / idea: アイデア
topics: [github, rust, oss, cli]
published: true
---

# はじめに
つい先日、[MinIOがDocker Imageの無料配布を停止したニュース](https://gigazine.net/news/20251023-minio-stops-distributing-free-docker-images/)が話題になりました。
OSSはメンテナの善意で提供されており、我々はsponsorをしていないものについては無料で使わせてもらっているということを改めて認識しなければならないニュースです。
一方で、普段使っているossすべてにsponsorをするほどの資金力はないという現実もあります。

## なら、せめてお世話になっているOSSには積極的にstarを残していきませんか？？

starの数が意外とOSSメンテナの人生への影響度が大きいという話は、昔[teppeis sanのブログ](https://teppeis.hatenablog.com/entry/2017/08/thank-you-stars)を読んでなるほどと思った記憶があります。

一方で、teppeis sanがブログで紹介してくださっている[thank-you-stars](https://github.com/teppeis/thank-you-stars)は僕も長らく愛用させていただいていますが、npmのリポジトリにしか適用できないことにもやもやがありました。
githubで検索してみると、goやcargo,haskellなどさまざまな言語やエコシステムむけにそれぞれ開発されているrepositoryが見つかりましたが、統合環境がありませんでした。

# というわけで、作りました

https://github.com/Kenzo-Wada/thanks-stars

手元のプロジェクトが依存しているパッケージ群を検出して、そのソースリポジトリにまとめてGitHubのスターを付けます！
Rustで書いた理由は単純に普段から筆者が良くしゃべる言語であり、parser周り扱うならserdeが慣れていたのと、並列実行などでパフォーマンスを追い求められそうというだけです。特に深い理由はないです。

---

## 対応エコシステム（2025-10-26 時点）

プロジェクトのルートで実行すると、以下のファイルを手掛かりに依存関係を検出します。

| エコシステム             | 主な検出ファイル                                                           |
| ------------------------ | -------------------------------------------------------------------------- |
| **Rust / Cargo**         | `Cargo.lock`, `Cargo.toml`                                                 |
| **Node.js**              | `package.json`                                                             |
| **Gradle (Java/Kotlin)** | `build.gradle`, `build.gradle.kts`, `gradle.lockfile`                      |
| **Python**               | `pyproject.toml`, `requirements.txt`, `Pipfile`, `Pipfile.lock`, `uv.lock` |
| **R (renv)**             | `renv.lock`                                                                |
| **Dart / Flutter**       | `pubspec.yaml`, `pubspec.lock`                                             |
| **composer (PHP)**       | `composer.json`, `composer.lock`                                           |
| **Ruby / Bundler**       | `Gemfile`, `Gemfile.lock`                                                  |

> 上記以外も対応していきたいので、Issueでの提案やcontribute大歓迎です！

---

## インストール方法

```bash
# brew
brew tap Kenzo-Wada/thanks-stars
brew install Kenzo-Wada/thanks-stars/thanks-stars
# npm
npm install -g thanks-stars
# cargo
cargo install thanks-stars
```

---

## 実行方法

プロジェクトのルートで実行するだけです。

```bash
cd your-project
thanks-stars
```

**標準実行の出力例：**

````bash
$ thanks-stars
⭐ Starred https://github.com/xxx/xxx via Cargo.toml
✅ Already starred https://github.com/xxx/xxx via package.json
...
✨ Completed! ⭐ Starred 10 repositories.```
````

**Dry-run（事前確認）出力例：**

````bash
$ thanks-stars --dry-run
⭐ Would star https://github.com/xxx/xxx via Cargo.toml
✅ Already starred https://github.com/xxx/yyy via package.json
...
✨ Dry run complete! ⭐ 1 repository would be starred, ✅ 1 already starred.```
````

---

# さいごに

thanks-starsの紹介ばかりになってしまいましたが、改めてOSSのメンテナに感謝して快適な開発体験を〜！
thanks-starsへのスターもよかったら残してってください！
