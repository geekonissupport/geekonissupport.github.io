# geekonis-site

Geekonis の公開ページ。**プライバシーポリシーのURLを用意するのが主目的**で、
Play Console の4アプリすべてに同じURLを入れる。

ビルド工程を持たない素のHTML/CSSにしてある。Jekyll のテーマも npm も要らないので、
GitHub Pages に置くだけで動く。

## 構成

| ファイル | 内容 |
|---|---|
| `index.html` | アプリ一覧とポリシーへの導線 |
| `privacy.html` | プライバシーポリシー（日本語）。**4アプリ共通** |
| `privacy-en.html` | 同（英語） |
| `style.css` | 共通スタイル。ライト/ダーク両対応 |
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

**公開済み。** 2026-10-17 に `https://geekonissupport.github.io/` と `/privacy-en.html` が
ともに 200 を返すことを確認した（トップページは `<html lang="en">` の英語版）。
以下は復旧・作り直しのときの手順。

1. GitHub の `geekonissupport` アカウントで公開リポジトリ `geekonissupport.github.io` を作る
2. このディレクトリの中身をそのまま push する
3. Settings → Pages → Source を `main` ブランチのルートにする
4. 数分後に `https://geekonissupport.github.io/` で見られるようになる
5. Play Console の「アプリのコンテンツ → プライバシーポリシー」に
   **`https://geekonissupport.github.io/privacy-en.html`** を入れる（4アプリとも同じ）

`.github.io` のリポジトリはユーザーサイト扱いになるため、パスにリポジトリ名が入らない。
アプリ側から参照するURLが短く安定する。

### ローカルのクローンは1つ（2026-10-22 時点）

**`D:\source\flutter\geekonis-site` はもう無い**（2026-10-22 に確認）。編集も公開も
`D:\source\geekonissupport.github.io`（`main`）で行う。下の表と説明は2026-10-17時点の記録。

### （記録）ローカルのクローンは2つあった（2026-10-17 に整理）

| 場所 | ブランチ | 役目 |
|---|---|---|
| `D:\source\flutter\geekonis-site`（ここ） | `master` → `origin/main` | 編集する場所。`backup_repos.ps1` の退避対象 |
| `D:\source\geekonissupport.github.io` | `main` | 公開用。認証付きURL（`https://geekonissupport@...`）でcloneしてある |

**2026-10-17 までこの2つはリモートを共有しておらず、別々の履歴を持っていた。**
こちら側に `origin` を足して `master:main` でpushし、公開用クローンを `git pull --ff-only` で
追従させて揃えた（両方とも `b2aacea`）。**以後はどちらで編集してもpush/pullで同期できる。**

- **4本のアプリと違って、このリポジトリだけはリモートを持っている。** つまり退避が
  GitHub にもある唯一のリポジトリ
- **ブランチ名が違う**（`master` と `main`）。既定の `push.default=simple` は名前が違うと
  pushを拒否するので、このリポジトリに `push.default=upstream` を設定した。
  **これで素の `git push` が通る**（設定しない場合は `git push origin master:main`）
- 編集はどちらか一方に決めて行う。両方で別々に直すと、また共通祖先の無い履歴になる
- **親リポジトリ（`D:\source\flutter`）もこのディレクトリのファイルを追跡している。**
  サイトを直すと**2つのリポジトリにコミットが要る**（ここと親）。片方だけ入れると、
  親の退避バンドルに古い中身が残る

### Playに入れるのは英語ページ（2026-09-17 決定）

Play のプライバシーポリシーURLは**アプリごとに1つで、言語別に分けられない**。
既定の言語を英語にすると決めている（`../RELEASE_PLAYBOOK.md` 6章）ので、
入れるのは `privacy-en.html` にする。英語ページの先頭から日本語ページへのリンクが
あるので、日本語の利用者も1クリックで辿れる。

## 公開前に必ずやること

- [x] **連絡先メールアドレスを記入する**（2026-09-17）。`geekonissupport@gmail.com` を
      `index.html` / `privacy.html` / `privacy-en.html` の3か所に入れた
- 個人名や既存の私用アドレスは使わない。屋号名義の新規アドレスを用意する
  （Play のストア掲載では連絡先が**公開される**ため）

## 更新のルール

- ポリシーを変更したら**制定日（Effective）を必ず改める**。日英の両方を揃える
- アプリの権限や通信先を変えたら、このページの表とPlayのデータセーフティ申告を
  同時に直す。片方だけ直すと申告と実態がずれる
- 実態の一次情報は `../RELEASE_PLAYBOOK.md` の「4. データセーフティ申告」にある表
