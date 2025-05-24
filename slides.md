---
title: "CSSカルーセル"
subtitle: "～CSS Overflow Module Level 5～"
author: "@totocalcio"
theme: seriph
layout: center
class: text-center
---

# CSSカルーセル
## CSS Overflow Module Level 5

<div class="abs-br m-6 flex gap-2">
  <a href="https://twitter.com/dir20634" target="_blank" alt="X" title="Open in X"
    class="text-xl slidev-icon-btn opacity-50 !border-none !hover:text-gray600">
    <carbon-logo-x />
  </a>
  <a href="https://github.com/totocalcio/slidev" target="_blank" alt="GitHub" title="Open in GitHub"
    class="text-xl slidev-icon-btn opacity-50 !border-none !hover:text-gray600">
    <carbon-logo-github />
  </a>
</div>

<!--
-->

---
transition: fade
---

<h1 class="flex flex-items-center gap-4"><img class="h-14 rounded-full" src="/images/avatar.jpg" alt="totocalcio アバター" >自己紹介</h1>

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
  - 好きなCSS関数はcolor-mix()（一年前と一緒）

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
まずは簡単に自己紹介をさせていただきます。
(自己紹介する)
-->

---
transition: slide-up
level: 2
---

## 今日話すこと

1. CSS Overflow Module Level 5とは？
2. CSS カルーセルとは？
3. ブラウザサポート状況
4. 実装方法
5. アクセシビリティに関する補足

---

## CSS Overflow Moduleについて
- overflowまわりの仕様をまとめたもの

## CSS Overflow Module Level 5とは？
- スクロールに関する様々な機能が追加された
  - 擬似要素 `::scroll-button()` や `::scroll-marker()`など

> 参考：[CSS Overflow Module Level 5](https://drafts.csswg.org/css-overflow-5/)

---

### カルーセルとは？

- よく見かける横スクロールのスライドショーや画像ギャラリーのこと

<br />

### カルーセルの構成要素
- スクロールコンテンツ
  - コンテンツそのもの
  - 主にリスト形式で実装される
- スクロールボタン
  - 前の要素、次の要素に移動する
  - 左矢印と右矢印のアイコンで実装されているようなやつ
- スクロールマーカー
  - ナビゲーションの役割があり、スクロールコンテンツへアクセスする
  - 円形インジゲーターのようなやつ

<br />

### CSS カルーセル
- カルーセルの実装は今まではライブラリを使用したり、JavaScriptを書いたりしていた。
- それが、**CSSのみで実装できるようになった！**

<style>
li {
  font-size: 1rem
}
</style>

---

## ブラウザサポート状況
### Chrome 135のリリースでサポート

- `::scroll-button()` と `::scroll-marker()`がChromeに実装された。

> 参考：[New in Chrome 135](https://developer.chrome.com/blog/new-in-chrome-135?hl=ja)

<br />

### その他ブラウザ

<iframe src="https://wpt.fyi/results/css/css-overflow?label=master&label=experimental&aligned&q=scroll-button" width="100%" height="300"></iframe>

---
layout: statement
class: text-center
---

実装例

---

## 1. リストを作成する

<div grid="~ cols-2 gap-8" class="mt-4">
```html
<ul>
  <li>item 1</li>
  <li>item 2</li>
  <li>item 3</li>
  <li>item 4</li>
  <li>item 5</li>
  <li>item 6</li>
  <li>item 7</li>
  <li>item 8</li>
  <li>item 9</li>
  <li>item 10</li>
</ul>
```
<ul>
  <li v-for="i in 10">
    item {{ i }}
  </li>
</ul>
</div>

---

## 2. アイテムを横並びにして横スクロールにする

<div grid="~ cols-2 gap-8" class="mt-4">
```html
<div class="carousel">
  <ul class="list">
    <li>item 1</li>
    <li>item 2</li>
    <li>item 3</li>
    <li>item 4</li>
    <li>item 5</li>
    <li>item 6</li>
    <li>item 7</li>
    <li>item 8</li>
    <li>item 9</li>
    <li>item 10</li>
  </ul>
</div>
<style>
.carousel {
  overflow-x: auto;
}
.list {
  display: flex;
  li {
    list-style-type:none;
  }
}
</style>
```
<div class="flex flex-col">
<div class="overflow-x-auto">
  <ul class="flex">
    <li v-for="i in 10" style="list-style-type:none" class="border">
      item {{ i }}
    </li>
  </ul>
</div>
</div>
</div>

---

## 3. スクロールボタンを追加する

<div grid="~ cols-2 gap-8" class="mt-4">
```html
<div class="carousel" >
  <ul class="list">
    <li>item 1</li>
    <li>item 2</li>
    <li>item 3</li>
    <li>item 4</li>
    <li>item 5</li>
    <li>item 6</li>
    <li>item 7</li>
    <li>item 8</li>
    <li>item 9</li>
    <li>item 10</li>
  </ul>
</div>
<style>
.carousel {
  overflow-x: auto;
  &::scroll-button(left) {
    content: "←" / "Prev";
  }
  &::scroll-button(right) {
    content: "→" / "Next";
  }
}
.list {
  display: flex;
  li {
    list-style-type:none;
  }
}
</style>
```
<div class="flex flex-col">
  <div>
    <div class="carousel overflow-x-auto mb-4">
      <ul class="flex">
        <li v-for="i in 10" style="list-style-type:none" class="border">
          item {{ i }}
        </li>
      </ul>
    </div>
  </div>
  <div>
    <ul>
      <li>overflowを定義している要素(今回でいえば<code>.carousel</code>)へ<code>::scroll-button()</code>疑似要素を定義する。</li>
      <li><code>::scroll-button()</code>のセレクタにleftかrightを設定する。</li>
      <li>
        <code>::scroll-button()</code>疑似要素の<code>content</code>にボタンとして表示するコンテンツを設定
        <ul><li>contentプロパティなので代替テキストを設定することも可能。</li></ul>
      </li>
    </ul>
  </div>
</div>
</div>

<style>
.carousel {
  &::scroll-button(left) {
    content: "←" / "Prev";
  }
  &::scroll-button(right) {
    content: "→" / "Next";
  }
}
</style>

<!--
left、rightは論理プロパティでも指定可能(inline-start, inline-end)
disabledやfocus-visibleといった擬似クラスによるスタイリングも可能
-->

---

## 4. スクロールマーカーを追加する

<div grid="~ cols-2 gap-8" class="mt-4">
```html
<div class="carousel" >
  <ul class="list">
    <li>item 1</li>
    <li>item 2</li>
    <li>item 3</li>
    <li>item 4</li>
    <li>item 5</li>
    <li>item 6</li>
    <li>item 7</li>
    <li>item 8</li>
    <li>item 9</li>
    <li>item 10</li>
  </ul>
</div>
<style>
.carousel {
  overflow-x: auto;
  &::scroll-button(left) {
    content: "←" / "Prev";
  }
  &::scroll-button(right) {
    content: "→" / "Next";
  }
  scroll-marker-group: after;
  &::scroll-marker-group {
    display: grid;
    place-content: center;
    grid-template-rows: 1rem;
    grid-auto-columns: 1rem;
    grid-auto-flow: column;
    gap: .5rem;
  }
}
.list {
  display: flex;
  li {
    list-style-type:none;
    &::scroll-marker {
      content: " " / "Marker";
      border: 1px solid red;
      border-radius: 50%;
      &:target-current {
        background-color: blue;
        border-color: blue;
      }
    }
  }
}
</style>
```
<div class="flex flex-col">
  <div>
    <div class="carousel overflow-x-auto mb-4">
      <ul class="flex list">
        <li v-for="i in 10" class="border">
          item {{ i }}
        </li>
      </ul>
    </div>
  </div>
  <div>
    <ul>
      <li><code>scroll-marker-group</code>でマーカーグループの位置を指定</li>
      <li>
        <code>::scroll-marker-group</code>と<code>::scroll-marker</code>それぞれにスタイルをあてる
        <ul>
          <li><code>::scroll-marker-group</code>はoverflow要素(今回でいえば<code>.carousel</code>)</li>
          <li><code>::scroll-marker</code>はアイテム要素(今回でいえば<code>li</code>)</li>
          <li><code>:target-current</code>擬似クラスで、現在表示中の状態のマーカースタイルも設定できる。</li>
        </ul>
      </li>
    </ul>
  </div>
</div>
</div>

<style>
.carousel {
  &::scroll-button(left) {
    content: "←" / "Prev";
  }
  &::scroll-button(right) {
    content: "→" / "Next";
  }
  scroll-marker-group: after;
  &::scroll-marker-group {
    display: grid;
    place-content: center;
    grid-template-rows: 1rem;
    grid-auto-columns: 1rem;
    grid-auto-flow: column;
    gap: .5rem;
  }
}
.list li{
  flex-shrink: 0;
  list-style-type: none;

  &::scroll-marker {
    content: " " / "Marker";
    border: 1px solid red;
    border-radius: 50%;
    &:target-current {
      background-color: blue;
      border-color: blue;
    }
  }
}
</style>

<!--
scroll-marker-group</code>の子要素に<code>::scroll-marker</code>がいるわけではないのでflexではなくgridでスタイリングすることになると思います。
-->

---

## 疑似要素のAOM確認

- tabなのにMarkerがどのコンテンツとリンクしてるかわからん。
- `::scroll-marker`と`::scroll-button`は`::before`, `::after`のような静的コンテンツではなく、インタラクティブ要素。
  - インタラクティブならインタラクティブなりのアクセシビリティ要件がある。
- AOMができる流れも説明したいけど割愛。今回のスクロールマーカーとスクロールボタンで擬似要素つくってスクリーンリーダーなどの支援技術にも公開される、だけ理解。
- アクセシビリティツリー
- `::scroll-marker-group`はrole tablistとして、`::scroll-marker`はrole tabとして公開されている。
  - 但し、CSSの仕様としては存在していない。
- アクセシビルな名前はcontentプロパティで指定する。ブラウザが自動的に設定するわけではないので、手動で設定する。
- `::scroll-button`はもちろんrole button。同様にアクセシブルな名前をつける必要がある。

## アクセシビリティ上の問題点

- タブウィジェットのはず
- でもtabpanelは存在しない
  - `::scroll-marker`の元となる要素がtabpanelに変わるはず。
  - でもそこ自動で書き換えるとulもlist roleではなくなる。
- ARIAの仕様でアクティブなタブに対応するタブパネルがレンダリングされないといけない(MUST)
- 気をつけないとtabのcontentはすべておなじnameになる
- スクロールマーカーグループは複数選択にはなっていない(multiselectable属性がfalseになっている)
  - 復数ならaia-selectedとaria-expandedを設定しないといけない
- ボタンは非活性なのにアクセシビリティ情報上はそうなっていない
- tabpanelだけはハードコーディングする必要がある

> 参考：[Carousel Gallery](https://chrome.dev/carousel/)
> 参考:[Are 'CSS Carousels' accessible?](https://www.sarasoueidan.com/blog/css-carousels-accessibility/)


### タブウィジェットのアクセシビリティ要件

- タブを作るにはtab, tabpanel, tablist ロールを使用する必要がある。

#### ARIA 仕様

- tab roleはtablistに含まれているか所有されていなければいけない
- タブがアクティブな場合、tabpanelがレンダリングされていなければいけない
- 単一選択が可能なタブリストの場合、ユーザーがタブパネルに関連付けられたタブを選択するまで、他のタブパネルを非表示にする必要がある(SHOULD)。
- 複数選択可能なタブは、仕様上ではhy当時されているtabpanelのaria-expanded属性がtrueに設定されていること、そして非表示になっている残りのtabpanelのaria-expanded属性がfalseに設定されていること。
- 選択されたタブはaria-selected属性がtrueに、非アクティブなタブ要素はfalseが設定されている必要がある(SHOULD)

### タブの種類

1. 自動的にアクティブ化されるタブ
  - タブがフォーカスを受け取ると、自動的にアクティブ化され、そのパネルが表示される
2. 手動でアクティブ化ｓるうタブ
  - ユーザーがスペースキーまたはEnterキーを押すことでタブをアクティブ化し、そのパネルを表示する

### Tabのキーボード操作要件

- Tab キーを押して、フォカースがタブリストに移動すると、フォーカスはアクティブなタブ要素に移動する。
- タブリストにフォーカスが含まれている場合、Tabキーを再度押すと、タブリストの外側のタブシーケンス内の次の要素にフォーカスが移動する。
- フォーカスがタブリスト内にある場合
  - 左カーソルキーで前のタブへ移動。フォーカスが最初のタブにある場合は最後のタブに移動
  - 右カーソルキーで次のタブへ移動。フォーカスが最後のタブにある場合は最初のタブに移動


## Overflow level5 仕様
1. スクロールコンテナーにスクロールマーカーグループを作成
2. グループ内の各スクロールマーカーがスクロールコンテナー内の項目に対応
3. マーカーがコンテナー内のスクロール位置を示すようにスタイルの設定が可能

## 仕組み
- `::scroll-marker-group`疑似要素はスタイル可能な要素
  - 暗黙的にフォーカス可能なfocusgroupとして定義される。
  - スクロールマーカー間を移動するには矢印キーを使用する。
  - radio groupのようなもの
  - `::scroll-marker`疑似要素のコンテナ
- `::scroll-marker`はリスト要素の先頭に追加されるが、支援技術にグループとして公開できるように、`::scroll-marker-group`へ収集される
  - ブラウザがmarkerをgroupへ集約するように再配置している。
  - DOM -> AOM
---

## おまけ

Adam いないなった
<!-- layout: iframe -->
<!-- <iframe src="https://chrome.dev/carousel/" width="100%" height="500"></iframe> -->

---

## 🧱 ブラウザ対応と注意点
- Chrome 135+ 対応
- Safari/Firefoxは未対応（2025年5月時点）
- Fallbackとの併用が必要な場合も

---

## ✅ まとめ
- CSSだけでカルーセルを作れる時代がきた！
- ::scroll-button() と ::scroll-marker() を使えばアクセシブルに！
- まだ対応状況に注意しつつ、積極的に試してこ！

---

---

## 🙌 Thank you！
Slides: https://example.com/your-slides
GitHub: https://github.com/your-name
