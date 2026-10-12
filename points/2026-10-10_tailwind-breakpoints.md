# tailwind-breakpoints

## 2026-10-10

### 気になったこと / 気づいたこと
- Tailwind の `md` って何?
- 公式を見るとブレークポイントが rem 単位で指定されているけど、どういうこと?

### 補足・解説
- `md:` は「画面幅 768px 以上で適用する」ブレークポイントの接頭辞。「タブレットだけ」ではなく、768px 以上のすべての画面に当たる。
- Tailwind はモバイルファースト。接頭辞なしのクラスは全画面幅に効き、`md:xxx` は 768px 以上で上書きする。公式も「`sm:` を『小さい画面で』ではなく『small ブレークポイント以上で』と考える」と説明している。
  - 例: `flex flex-col md:flex-row` → スマホでは縦並び、768px 以上では横並び(`app/page.tsx:12`)
  - 例: `hidden md:block` と `block md:hidden` で、画像を PC 用とスマホ用で出し分けている(`app/page.tsx:37`, `app/page.tsx:45`)
- デフォルトのブレークポイント: `sm` 640px / `md` 768px / `lg` 1024px / `xl` 1280px / `2xl` 1536px
- rem 表記について:
  - 公式サイト(v4)では `md` = `48rem`(`@media (width >= 48rem)`)と定義されている。1rem = 16px(ブラウザのデフォルト)なので 48 × 16 = 768px で、値は v3 と同じ。
  - v3 のドキュメントでは px(`@media (min-width: 768px)`)で定義されていた。
  - **このプロジェクトは `tailwindcss` 3.4.17(`package.json:20`)なので、実際には px 定義のほうが使われている。**
  - rem にすると、ユーザーがブラウザの文字サイズを大きくしたとき、ブレークポイントもそれに合わせて大きくなる(例: 20px 設定なら `md` は 960px)。文字が大きいのに狭いカラムに押し込まれるのを防げる。
  - メディアクエリ内の相対単位は、ページの CSS(`html { font-size: ... }`)ではなく、初期値(ブラウザ/ユーザー設定)が基準になる(Media Queries Level 4 §1.3)。そのため、自分の CSS でブレークポイントがずれることはない。

### 参考リンク
- [Responsive design - Tailwind CSS(v4)](https://tailwindcss.com/docs/responsive-design#overview) — rem 表記のデフォルトブレークポイント一覧
- [Responsive design - Tailwind CSS(v4)#working-mobile-first](https://tailwindcss.com/docs/responsive-design#working-mobile-first) — モバイルファーストの考え方と「接頭辞なし = 全画面」の説明
- [Responsive design - Tailwind CSS v3](https://v3.tailwindcss.com/docs/responsive-design#overview) — v3 では px 定義(このプロジェクトのバージョン)
- [<length> - MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/length#rem) — rem はルート要素の font-size が基準で、一般的なデフォルトは 16px、ユーザー設定で変わりうる
- [Media Queries Level 4 §1.3 Units](https://www.w3.org/TR/mediaqueries-4/#units) — メディアクエリ内の相対単位は、ページのスタイルではなく初期値(ユーザー設定)が基準
