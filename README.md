# web/ — スマホ用 AI聞き手（ブラウザ版）

スマホ(Pixel/Android Chrome)で、AIが質問を読み上げ→その場で文字起こし→保存できるWebアプリ。
出てきたテキストは「コピー」か「共有」で Claude に渡す → 本の章に取り込まれます。

```
index.html             アプリ本体（これ1枚で動く）
manifest.webmanifest   ホーム画面に追加用
sw.js                  オフライン用サービスワーカー
icon.svg               アイコン
```

## 使い方（スマホ）
1. 公開URLを **Android の Chrome** で開く
2. （任意）メニュー →「ホーム画面に追加」でアプリのようになる
3. 質問を選ぶ → AIが読み上げる → **🎤タップして話す** → もう一度タップで停止
4. 文字起こしを確認（その場で直せる）→ **💾保存**
5. 最後に **📋まとめてコピー** か **📤共有** で Claude に渡す

> ※ 文字起こしはネット接続が必要（Googleの音声認識を使用）。読み上げはオフラインでもOK。
> ※ iPhoneのSafariは「その場で文字起こし」非対応。その場合はキーボードのマイクで入力。

## 公開のしかた（https が必須：マイク許可のため）

### 方法1: GitHub Pages（無料・おすすめ）
このリポジトリを GitHub に上げて、Settings → Pages → Branch を `main` / フォルダを `/web`(または root) に設定。
数分後に `https://<ユーザー名>.github.io/<リポジトリ>/` で開けます。

### 方法2: Netlify / Cloudflare Pages
`web/` フォルダをドラッグ&ドロップ、または連携でデプロイ。

### 方法3: 既存サイト(stella-app.jp 等)
`web/` の中身をサーバーの公開ディレクトリにアップロード。

## ローカルで確認（PC）
```
python -m http.server 5517 --directory web
```
→ PCのブラウザで http://localhost:5517 （PCのChromeなら文字起こしも試せます）

## カスタマイズ
- 質問を変える/足す … `index.html` の `CORE` / `THEME` 配列（[../04_interview_questions.md](../04_interview_questions.md) と対応）
- 色・文字サイズ … `index.html` 上部の `:root` 変数
