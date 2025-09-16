# twitter-clone
twitterの技術に興味を持ったため。
フロントエンドnext.js バックエンドexpress 
使用言語　typescript
DB　開発: SQLite 本番: Neon(PostgreSQL)
ORM: Prisma
認証: Clerk
型検証: Zod

～環境構築～
npx create-next-app@latest フォルダ名 --typescript --eslint

npm install @clerk/nextjs axios 　　　　
axios(HTTPリクエストを送るためのライブラリ　fetchの便利版)

.envファイルをプロジェクト直下に作る（環境変数設定用）
.env.local
→ 開発環境専用（Gitに乗らない）
.env.development
→ 開発用（共有したい場合に使う）
.env.production
→ 本番用
.env.test
→ テスト用

.envファイルの内容（clerkにログインしてコピー）
NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY
公開しても良いキー（フロントエンドで使う用）
名前に NEXT_PUBLIC_ がついている変数は ブラウザ側にも渡る
Clerk のUIコンポーネントやログイン画面を表示する時に必要
CLERK_SECRET_KEY
検証用key　(公開してはいけない）

：Clerkの仕組み：
[ブラウザ] ---ログイン---> [Clerkサーバー]
      ←JWT発行/返却
[ブラウザ] ---JWT付きリクエスト---> [Next.js API]
                                      |
                                      | CLERK_SECRET_KEYで署名検証
                                      v
                                [認証OKなら処理実行]

app/layout.tsx　MyAppコンポーネント（全ページ共通の「レイヤーコンポーネント」、全ページに設定が適応される）にClerkProvider（ClerkProvider は 認証のコンテキスト を提供してくれるコンポーネント）
import { ClerkProvider } from "@clerk/nextjs";
import type { AppProps } from "next/app";

function MyApp({ Component, pageProps }: AppProps) {
  return (
    <ClerkProvider {...pageProps}>
      <Component {...pageProps} />
    </ClerkProvider>
  );
}
export default MyApp;



