---
theme: bricks
background: https://cover.sli.dev
title: Create a custom toggle switch
class: text-center
drawings:
  persist: false
transition: slide-left
mdc: true
fonts:
  serif: Yusei Magic
  mono: Fira Code
---

# 自作トグルスイッチ

Create a custom toggle switch

<!--
speaker note
-->

---
transition: fade-out
---

# 自己紹介

- 🏢 **会社**
  - 株式会社ラクス
- 👔 **職種**
  - フロントエンドエンジニア
- 🧑‍💻 **名前**
  - 亀ノ上 孝雄
- 🐰 **アカウント**
  - ととかるちょ(とと) / totocalcio
- 🦎 **ペット**
  - うさぎ、フトアゴヒゲトカゲ、ヒョウモンリクガメ
- 🐢 **一言**
  - CSS見てる時が一番落ち着く

<div class="absolute right-20 top-30 grid grid-cols-3 gap-4">
  <figure class="h-33 aspect-ratio-square overflow-hidden rounded-full">
    <img
      class="w-100 h-full object-cover object-top"
      src="/images/ginchan.jpg"
      alt="うさぎのぎんちゃんが小松菜を食べている"
    />
    <figcaption class="w-33 absolute top-33 text-center text-blue-700">ぎん</figcaption>
  </figure>
  <figure class="h-33 aspect-ratio-square overflow-hidden rounded-full">
    <img
      class="w-100 h-50 object-cover image-juzo"
      src="/images/juzo.jpg"
      alt="フトアゴヒゲトカゲのじゅうぞうがカメラ目線で見ている"
    />
    <figcaption class="w-33 absolute top-33 text-center text-blue-700">じゅうぞう</figcaption>
  </figure>
  <figure class="h-33 aspect-ratio-square overflow-hidden rounded-full">
    <img
      class="w-100 h-50 object-cover image-kanta"
      src="/images/kanta.jpg"
      alt="ヒョウモンリクガメのかんたが少し上を見ている"
    />
    <figcaption class="w-33 absolute top-33 text-center text-blue-700">かんた</figcaption>
  </figure>
</div>

<style>
h1 {
  background-color: #2B90B6;
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 20%);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
.image-juzo {
  object-position: left -1rem top -1rem;
}
.image-kanta {
  object-position: left -2.5rem top 0;
}
</style>

<!--
speaker note
-->

---
transition: slide-up
level: 2
layout: image
image: /images/vuefes2024.png
backgroundSize: contain
---

<span v-mark.circle.red="1" class="absolute top-5 right-12 w-12 h-8" aria-hidden="true"></span>

<!--
speaker note
-->

---

<div grid="~ cols-2 gap-4">
<div>

# 機能

- クリックする度に言語を切り替えるスイッチ
- [Nuxt I18n](https://i18n.nuxtjs.org/) を使用する。

## Nuxt I18n

Vue i18n ベースの Nuxt 用のモジュール

- Vue Fes Japan2024の使用方法
  - URLを`https://example.com/en/sample`のように、`/en/`を付与し、ソースコード内では`$t(title)`のように呼び出す
  - 別途定義された`json` ファイルを参照して表示

</div>
<div>

<img
  class="mt-8 mb-20"
  src="/images/feature-toggle.png"
  alt="トグルスイッチを切り替えるイメージ画像"
/>

```json
// ja.json
{
  “title”: “タイトル”,
}
```

```json
// en.json
{
  “title”: “Title”,
}
```

```vue
<h1>{{ $t('title') }}</h1>
```

</div>
</div>

<!--
speaker note
-->

---

# 実装方針検討

<v-clicks>

- URLが変わるから anchor 要素かな…
- いや、JavaScriptでパスを書き換えているだけだから、別に画面遷移というわけではないか…
- ほな、ボタンか…
- トグルスイッチをボタンかぁ…
- `<input type="checkbox">` を拡張するか…？
- `<input type="checkbox">` でスイッチ…
- <span class="text-red-500">`<input type="checkbox" switch>`</span> !!!

</v-clicks>

<style>
.slidev-vclick-target {
  transition-duration: 0.75s;
}
</style>

<!--
speaker note
-->

---

# `<input type="checkbox" switch>`

`checkbox` に `switch` 属性を指定することで、スイッチUIを実現できる標準機能。

<div grid="~ cols-2 gap-8">
<div>

<div class="mt-4">
  <input type="checkbox" id="lang" switch/>
  <label for="lang">言語切り替え</label>
</div>

```html
<div>
  <input type="checkbox" id="lang" switch />
  <label for="lang">言語切り替え</label>
</div>
```

</div>
<div>

<v-clicks every="2">

<div class="mt-4">
  <input class="lang-switch" type="checkbox" id="lang-red" switch/>
  <label for="lang-red">言語切り替え</label>
</div>

```html
<div>
  <input type="checkbox" id="lang" switch />
  <label for="lang">言語切り替え</label>
</div>
<style>
  input[type="checkbox"][switch] {
    accent-color: red;
  }
</style>
```

</v-clicks>

</div>
</div>

<style>
.lang-switch {
  accent-color: red;
}
</style>

<!--
speaker note
-->

---
layout: quote
transition: slide-up
level: 2
---

<h1 role="generic">やっぱり HTML 標準が考慮も<br>少なくなるし安心だよね😁</h1>

<!--
speaker note
-->

---
layout: fact
---

<h1 role="generic">がっ……駄目っ……!</h1>

<!--
speaker note
-->

---
layout: image
image: /images/wpt-switch.png
backgroundSize: contain
---

<span v-mark.underline.red="1" class="absolute top-25 left-65 w-62 h-1" aria-hidden="true"></span>

<span v-mark.box.red="2" class="absolute top-68 right-2 w-40 h-50" aria-hidden="true"></span>

<!--
speaker note
-->

---
layout: quote
transition: slide-up
level: 2
---

<h1 role="generic">トグルスイッチをアクセシブルに実装するのはどうすれば<br>いいんだろう？🤔</h1>

<!--
speaker note
-->

---
layout: fact
---

<h1 role="generic">そういうときはだいたいここ</h1>

<!--
speaker note
-->

---
transition: slide-up
layout: image
image: /images/apg.png
backgroundSize: contain
---

<div class="visually-hidden">ARIA Authoring Practices Guide トップページのスクリーンショットが背景画像に設定されている</div>
<span v-mark.circle.red="1" class="absolute top-21 left-30 w-16 h-8" aria-hidden="true"></span>

<!--
speaker note
-->

---
transition: slide-up
layout: quote
---

<h1 role="generic">ある</h1>

<img class="mx-auto" src="/images/apg-ss-switch-card.png" alt="ARIA Authoring Practices GuideのPatternページに表示されているSwitchコンポーネントカードのスクリーンショット" >

<!--
speaker note
-->

---
transition: slide-up
layout: quote
---

<h1 role="generic">(サンプルコードも)ある</h1>

<img class="mx-auto" src="/images/apg-ss-switch-examples.png" alt="ARIA Authoring Practices GuideのSwitch Patternページに表示されているExamplesのスクリーンショット" >

<!--
speaker note
-->

---
layout: fact
---

<h1 role="generic">(機能解説も)ある</h1>

<!--
speaker note
-->

---
transition: slide-up
layout: image
image: /images/apg-ss-switch-feature.png
backgroundSize: contain
---

<div class="visually-hidden">ARIA Authoring Practices Guide Switch Examplesページのアクセシビリティ機能に関する説明のスクリーンショットが背景画像に設定されている</div>
<span v-mark.underline.red="1" class="absolute top-25 left-150 w-54 h-1" aria-hidden="true"></span>
<span v-mark.underline.red="1" class="absolute top-29 left-44 w-82 h-1" aria-hidden="true"></span>

<span v-mark.underline.red="1" class="absolute top-38 left-44 w-162 h-1" aria-hidden="true"></span>
<span v-mark.underline.red="1" class="absolute top-43 left-44 w-51 h-1" aria-hidden="true"></span>

<span v-mark.underline.red="1" class="absolute top-48 left-44 w-162 h-1" aria-hidden="true"></span>
<span v-mark.underline.red="1" class="absolute top-52 left-44 w-124 h-1" aria-hidden="true"></span>

<span v-mark.underline.red="1" class="absolute top-77 left-44 w-162 h-1" aria-hidden="true"></span>
<span v-mark.underline.red="1" class="absolute top-81 left-44 w-47 h-1" aria-hidden="true"></span>

<!--
speaker note
-->

---

# 意識したこと①

<br>
<dl>
<dt class="text-indigo-700 mb-8 text-bold">
視覚障害や認知障害を持つユーザーがスイッチの状態を理解しやすくするために、状態 (オンまたはオフ) に相当するテキストがグラフィカルな状態インジケーターの隣に表示されます。
</dt>
<v-clicks>
<dd class="list-item ml-4 mb-2" v-motion :initial="{ x: -80 }" :enter="{ x: 0 }" :leave="{ x: 80 }">
Example ではトグルスイッチのラベルが隣にあって、確かに判断しやすいけど、デザインフェーズの課題なのでスルーする。</dd>
<dd class="list-item ml-4 mb-2">実際は課題というより、今回のデザインはラベルと一体化しているというものであるので、単純な（ラベルのない）トグルスイッチよりはわかりやすいと思う。</dd>
<dd class="list-item ml-4 mb-2" v-motion :initial="{ x: -80 }" :enter="{ x: 0 }" :leave="{ x: 80 }">
このような課題は、デザイン段階でアクセシブルかどうかのチェックが必要だから、デザインレビューであったり、アクセシビリティテストのシフトレフトが話題にあがったりするんだな、と感じた。</dd>
</v-clicks>
</dl>

<!--
speaker note
-->

---

# 意識したこと②

<br>
<dl>
<dt class="text-indigo-700 mb-8 text-bold">
注:スクリーンリーダーによる状態の冗長なアナウンスを防ぐため、状態のテキストインジケーターはによって支援技術から非表示になっていますaria-hidden。
</dt>
<v-clicks>
<dd class="list-item ml-4 mb-2" v-motion :initial="{ x: -80 }" :enter="{ x: 0 }" :leave="{ x: 80 }">
たしかにDOMを全部読み上げたらむしろわかりづらい
</dd>
<dd class="list-item ml-4 mb-2 text-red-700 text-bold" v-motion :initial="{ x: -80 }" :enter="{ x: 0 }" :leave="{ x: 80 }">
トグルスイッチであることと、現在の状態が伝われば良い。
</dd>
</v-clicks>
</dl>

<!--
speaker note
-->

---

# 意識したこと③

<br>
<dl>
<dt class="text-indigo-700 mb-8 text-bold">
間隔、境界線の幅、塗りつぶしは、ブラウザやオペレーティングシステムの高コントラスト設定が有効になっている場合を含め、視覚障害のある人がグラフィックの状態を視認し、識別できるようにするために重要です。
</dt>
<v-clicks>
<dd class="list-item ml-4 mb-2" v-motion :initial="{ x: -80 }" :enter="{ x: 0 }" :leave="{ x: 80 }">
初期デザインでは、axeDevtools を実行したところ、コントラスト比に問題があった。
</dd>
<dd class="list-item ml-4 mb-2 text-red-700 text-bold" v-motion :initial="{ x: -80 }" :enter="{ x: 0 }" :leave="{ x: 80 }">
デザイナに報告してなおしてもらった。
</dd>
</v-clicks>
</dl>

<!--
speaker note
-->

---

# 意識したこと④

<br>
<dl>
<dt class="text-indigo-700 mb-8 text-bold">
スイッチを操作する際の認識性を高めるために、視覚的なキーボード フォーカスとホバーはCSS:hoverと:focus疑似クラスを使用してスタイル設定されます。
</dt>
<v-clicks>
<dd class="list-item ml-4 mb-2" v-motion :initial="{ x: -80 }" :enter="{ x: 0 }" :leave="{ x: 80 }">
Exampleページの機能に記載されている、スタイルの課題が全て解決しているわけではないが、少なくともホバー時とフォーカス時でスタイルを設定し、それぞれ認識できるようにはした。
</dd>
<dd class="list-item ml-4 mb-2" v-motion :initial="{ x: -80 }" :enter="{ x: 0 }" :leave="{ x: 80 }">
実務でも実装のタイミングで都度インタラクションの相談することはあるので、最初のデザイン段階で相談して詰めておきたいと、改めて思った。
</dd>
</v-clicks>
</dl>

<!--
speaker note
-->

---

# 結果こうなった

<div grid="~ cols-2 gap-8">
<div>

```html
<button
  type="button"
  role="switch"
  aria-label="translate english"
  :aria-checked="isChecked"
  @click="onSwitch"
>
  ...
</button>
```

</div>
<div>

<figure>
<img src="/images/swich-aom.png" alt="switchコンポーネントのAOM" >
</figure>

</div>
</div>

<Arrow x1="210" y1="182" x2="530" y2="396" />
<Arrow x1="330" y1="200" x2="550" y2="310" />
<Arrow x1="300" y1="220" x2="530" y2="460" />

<!--
speaker note
-->

---

# まとめ

<v-clicks>

- HTML標準要素ではないコンポーネントを開発する際に、ARIA Authoring Practices Guide (APG)を参考にした。
  - 改めて見直すとまだ調整したいところがある。
  - 自身の課題として、今後活かしていきたい。
- <span class="text-bold">Vue Fes Japan 2024 は 2024/10/19 開催。チケット販売中。</span>
  - このスライドも `Vue.js`で作成されています。

</v-clicks>

<div v-after class="mt-6">

<h2 class="mb-4">参考</h2>

- [ARIA Authoring Practices Guide (APG)](https://www.w3.org/WAI/ARIA/apg/)
- [Vue Fes Japan 2024](https://vuefes.jp/2024/)

</div>

<!--
speaker note
-->

---
layout: statement
class: text-center
---

# ありがとうございました

<TheSwitch />

<PoweredBySlidev mt-10 />

<!--
speaker note
-->
