# longshipworks.github.io

アプリのサポートページとプライバシーポリシー。<https://longshipworks.github.io/>

## 原本がどこにあるか（ファイル単位で分かれている）

| 場所 | 原本 | 直接編集 |
|---|---|---|
| ルート（`index.html` / `style.css` / `README.md`） | **このリポジトリ** | してよい |
| `<アプリ名>/` 以下 | **各アプリのリポジトリ**（`docs/store/site/<アプリ名>/`） | **してはいけない** |

アプリのページをここで直すと、次にそのアプリが `publish-site.sh` を走らせた時点で
上書きされて消える。2か所で書けば必ずずれる。

ルートはどのアプリのものでもないので、ここが原本。アプリが増えたら
`index.html` に1件足す（この作業だけは手で行う）。

## 公開中のページ

| ページ | URL | 原本のリポジトリ |
|---|---|---|
| Longship Works | <https://longshipworks.github.io/> | ここ |
| うつしてぬりえ サポート | <https://longshipworks.github.io/utsushite-nurie/> | `utsushite-nurie`（非公開） |
| うつしてぬりえ プライバシーポリシー | <https://longshipworks.github.io/utsushite-nurie/privacy.html> | `utsushite-nurie`（非公開） |

開運手帖は別リポジトリ `longshipworks/kaiun-techo-legal` のまま
（<https://longshipworks.github.io/kaiun-techo-legal/>）。
配布済みバイナリにそのURLが焼かれていて 404 にできないため、ここへは統合していない。

## 新しいアプリのページを足す手順

1. アプリのリポジトリに `docs/store/site/<アプリ名>/` を作り、HTML を置く。
   スタイルは共通の `style.css` を使う（`<link rel="stylesheet" href="../style.css">`）。
   ヘッダーとフッターのリンクは `../` でルートへ戻す。既存の
   `utsushite-nurie/index.html` をひな形にするのが早い。
2. `utsushite-nurie/scripts/publish-site.sh` をコピーし、先頭の `SLUG` を変える。
   同期は `<アプリ名>/` の中だけに閉じているので、他アプリを壊さない。
3. このリポジトリの `index.html` にアプリの見出しとリンクを足して push する。
4. App Store Connect のサポートURL・プライバシーポリシーURLに新URLを登録する。

**App Store Connect に登録したURLが 404 になると審査が止まる。**
URL を決めるのは公開より前、アプリのリポジトリを作る時点で行うこと。
一度ストアに出したURLは、配布済みバイナリの中に残るので後から変えられない。

## CSS のキャッシュ

GitHub Pages は `Cache-Control: max-age=600` を返すため、`style.css` を差し替えても
一度見た人のブラウザには古い見た目が残る。`publish-site.sh` が送信時に全HTMLの
`style.css` へ中身の指紋（`?v=xxxxxxxx`）を打ち直している。
`style.css` をここで直接編集したときは、どれか1つのアプリの `publish-site.sh` を
走らせて指紋を打ち直すこと。
