# プロジェクトのフォルダ構成

## 2026-10-10

### 気になったこと / 気づいたこと
- 最適なプロジェクトフォルダ構成や、ベストプラクティス的なものはあるのか気になった。

### 補足・解説
- Next.js 公式ドキュメント(Project Structure)の立場は「**唯一の正解はない**。チーム内で一貫していればよい」。
- そのうえで、公式は代表的な3つの方針を紹介している:
  1. **`app/` の外にまとめる** — `app/` はルーティング専用にし、コンポーネントや処理は `src/components`、`src/lib` などに置く。
  2. **`app/` 直下のトップレベルフォルダにまとめる** — `app/lib`、`app/ui` のように置く。
  3. **機能・ルートごとに分ける(colocation)** — 共通のものは上位に、特定のページでしか使わないものはそのルートのフォルダに置く。
- このプロジェクト(公式チュートリアル)は **2 の方針**:
  - `app/lib/` … データ取得(`data.ts`)、型(`definitions.ts`)、ユーティリティ(`utils.ts`)
  - `app/ui/` … UI コンポーネント。`dashboard/`、`invoices/`、`customers/` のように機能ごとにサブフォルダで分けている
- `app/` の中にファイルを置いても大丈夫な理由: URL として公開されるのは `page.tsx` や `route.ts` があるフォルダだけ。`app/ui/button.tsx` のようなファイルにはアクセスできない。
  - 逆に `app/query/route.ts`、`app/seed/route.ts` は `route.ts` があるので `/query`、`/seed` という API として公開される。
- 構成を整理するための Next.js の機能:
  - **Private Folder**(`_components` のように `_` で始める)… ルーティングの対象から明示的に外す。
  - **Route Group**(`(dashboard)` のように `()` で囲む)… URL に影響させずにルートをグループ化する。グループごとに別の layout を使うこともできる。
  - **`src/` ディレクトリ** … `app/` を `src/app/` に置き、設定ファイルと分けられる。

### 参考リンク
- [Project structure and organization | Next.js](https://nextjs.org/docs/app/getting-started/project-structure)
  - [Organizing your project](https://nextjs.org/docs/app/getting-started/project-structure#organizing-your-project) — 「Next.js is **unopinionated** about how you organize…」(構成に決まった正解はない)
  - [Examples](https://nextjs.org/docs/app/getting-started/project-structure#examples) — 代表的な3つの方針(Store project files outside of `app` / Store project files in top-level folders inside of `app` / Split project files by feature or route)と「自分とチームに合う方針を選び、プロジェクト全体で一貫させる」という結論
  - [Colocation](https://nextjs.org/docs/app/getting-started/project-structure#colocation) — `page.js` / `route.js` があるときだけルートが公開される(`app/` 内に安全に置ける理由)
  - [Private folders](https://nextjs.org/docs/app/getting-started/project-structure#private-folders) / [Route groups](https://nextjs.org/docs/app/getting-started/project-structure#route-groups) / [`src` folder](https://nextjs.org/docs/app/getting-started/project-structure#src-folder) — 構成整理のための機能

### 未解決・あとで調べる
- 規模が大きくなったとき、どの方針が扱いやすいか(feature 単位で分ける構成との比較)。
