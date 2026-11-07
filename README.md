# geekonis-site

ScoreSnap の公開ページ。**プライバシーポリシーのURLを用意するのが主目的**で、
Play Console のストア掲載に同じURLを入れる。

ビルド工程を持たない素のHTML/CSSにしてある。Jekyll のテーマも npm も要らないので、
GitHub Pages に置くだけで動く。

## 構成

| ファイル | 内容 |
|---|---|
| `index.html` | ScoreSnap の紹介とポリシーへの導線 |
| `apps/scoresnap.html` | 製品ページ |
| `scoresnap-privacy-en.html` / `-ko.html` | プライバシーポリシー（英語・韓国語） |
| `scoresnap-terms-en.html` / `-ko.html` | 利用規約（英語・韓国語） |
| `style.css` | 共通スタイル。ライト/ダーク両対応 |
| `app-ads.txt` | AdMob のアプリ所有者確認。**消すと広告配信が制限される** |
| `google4c71cef2db3beb6e.html` | Search Console の所有権確認。**中身は1行で、消さない**（下記） |

## Search Console の所有権確認（2026-10-02）

`github.io` のドメインは自分のものではないのでDNS方式は使えず、**URLプレフィックス方式**で
`https://geekonissupport.github.io/` を登録する。確認方法は「HTMLファイル」で、
Googleが渡す `google<ランダム>.html` をリポジトリの**ルートにそのまま置く**だけ
（ビルド工程が無いので加工は不要）。

- 登録に使うGoogleアカウントは **Play Console と同じもの**にする。同じなら、Play Console の
  ストアリスティングからのサイト所有権のリクエストが自動で承認される
- **確認ファイルは置いたままにする。** 消すと所有権の確認が外れる
- 公開は数十秒〜数分遅れる（2026-10-02の実測で約80秒）。
  `https://geekonissupport.github.io/google4c71cef2db3beb6e.html` が 200 を返してから
  Search Console の「確認」を押す

## 公開手順

**公開済み。** 2026-10-17 に `https://geekonissupport.github.io/` が 200 を返すことを確認した
（トップページは `<html lang="en">` の英語版）。以下は復旧・作り直しのときの手順。

1. GitHub の `geekonissupport` アカウントで公開リポジトリ `geekonissupport.github.io` を作る
2. このディレクトリの中身をそのまま push する
3. Settings → Pages → Source を `main` ブランチのルートにする
4. 数分後に `https://geekonissupport.github.io/` で見られるようになる
5. Play Console の「アプリのコンテンツ → プライバシーポリシー」に
   **`https://geekonissupport.github.io/scoresnap-privacy-en.html`** を入れる

`.github.io` のリポジトリはユーザーサイト扱いになるため、パスにリポジトリ名が入らない。
アプリ側から参照するURLが短く安定する。

## 編集場所は1つ

編集も公開もこのディレクトリ（`main`）で行う。**このリポジトリだけがリモート（GitHub）を
持つ**ので、退避がGitHubにもある唯一のリポジトリでもある。

- 以前は親リポジトリ側にも複製（`geekonis-site`）があり2か所にコミットが要ったが、
  2026-10-22にここ1つへ寄せた。退避はこのディレクトリを直接バンドルしている
- `push.default=upstream` を設定してある（ブランチ名が `main` で揃う前の名残）

## Playに入れるのは英語ページ（2026-09-17 決定）

Play のプライバシーポリシーURLは**アプリごとに1つで、言語別に分けられない**。
既定の言語を英語にすると決めているので、入れるのは英語版にする。
英語ページの先頭から韓国語ページへのリンクがある。
