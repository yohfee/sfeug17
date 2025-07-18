---
marp: true
theme: gaia
class: invert
---

## id:yohfee

株式会社はてな

Mackerel 開発チーム

アプリケーションエンジニア

![bg right](./images/yohfee.jpg)

---

# 最高の AI 画像生成アプリを作ろう

Sendai Frontend Meetup #17

---

<!-- _class: invert lead -->

## ローカル AI 画像生成してますか？

---

## ローカル AI 画像生成のいいところ

- 爆速
- 無制限
- 実質無料
- モデルを自由に選択できる
- 冬は暖房代わりになる
  - https://yohfee.hatenadiary.org/entry/2024/12/21/075305

---

## ローカル AI 画像生成といえば

- AUTOMATIC1111 Stable Diffusion Web UI
  - https://github.com/AUTOMATIC1111/stable-diffusion-webui
- ComfyUI
  - https://github.com/comfyanonymous/ComfyUI
- とか

---

## ComfyUI とは

ノードを繋げてパイプラインを組み立てるやつ

![bg](./images/comfy.png)

---

## ここがつらい

- 独自の世界観なので慣れるまでたいへん
- 組み込みノードの小回りが利かない
- プログラマブルなことは難しい
- 拡張機能が自作できるけど Python
- などなど

頑張って複雑なワークフローを組み立てたり
拡張機能をインストールして使ったりすれば
できるかもしれないけど...

---

## 実は API を有効化できる

- `--listen` オプションをつけて起動する
  - 必要に応じて `--enable-cors-header` も
- 公式ドキュメントは無い？
  - https://github.com/zigzagGmbH/VW-AA-ComfyUI-Workflow-Executor/blob/main/docs/COMFYUI_API.md がそれなりに書いてある
- 公式サンプルならちょっとだけある
  - https://github.com/comfyanonymous/ComfyUI/tree/master/script_examples

---

<!-- _class: invert lead -->

## 基本的には `POST /queue` に JSON を投げて
## WebSocket で進捗を眺めるだけ

---

<!-- _class: invert lead -->

## API があるなら何でも作れるね！

---

<!-- _class: invert lead -->

## では「最高の AI 画像生成アプリ」とは？

---

<!-- _class: invert lead -->

## そんなものはない

---

<!-- _class: invert lead -->

## 解決したい課題を倒せばいい

---

<!-- _class: invert lead -->

## 一つのことを行い、
## またそれをうまくやるプログラムを書け。

UNIX哲学

---

## これまで作った(広義の)フロントエンドたち

- SPA Webアプリケーション (F#, React)
- Chrome 拡張 (Vanilla JS)
- コマンドラインアプリケーション (F#, Node.js)
- Windows デスクトップアプリケーション (WinUI3)

---

## 無限にランダムな画像を生成して眺めたい

- 課題
  - 複数の処理をエンキューできるが常に全力で GPU が稼働し続けてしまう
  - 室温もどんどん上昇していく地獄
  - 更新ペースは遅くていい
- 解決
  - 任意の間隔でエンキューできるようにした

無限スライドショーができて最高！

---

## 同じパラメータでプロンプトの一部だけが異なる画像を生成したい

- 課題
  - ワークフローごとに変えられる範囲に制限がある
  - ノード自体の編集がめんどくさい
- 解決
  - プロンプトをテンプレート化して一回の実行で同じパラメータで複数エンキューできるようにした

バリエーションの比較が便利になって最高！

---

## 同じパラメータで複数の異なるサイズの画像を生成したい

- 課題
  - 画像サイズノードごとにパイプラインが必要
  - 画像サイズノードから先のパイプラインは全部同じなのに
- 解決
  - パラメータ JSON をテンプレート化して複数サイズ分を並列に生成できるようにした

重複が無くなり編集が楽ちんになって最高！

---

## カタログから画像を生成したい

- 課題
  - モデルの学習セットが CSV で配布されている
  - プロンプトにその作品とキャラクターを含めると精度が上がる
  - 数万行の CSV を毎回読みたくないし探すのも大変
- 解決
  - DuckDB にインポートして検索可能にした
  - プロンプトをテンプレート化して埋め込みできるようにした
  - ついでにお気に入り登録もできるようにした

なんかいろいろできて最高！

---

<!-- _class: invert lead -->

## 基本的には `POST /queue` に JSON を投げて
## WebSocket で進捗を眺めるだけ

---

<!-- _class: invert lead -->

## 君の最高の AI 画像生成アプリ、今すぐビル
## ド
