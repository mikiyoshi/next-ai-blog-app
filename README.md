# Next.js AI blog

## Next.js Installation
[Next.js](https://beta.nextjs.org/docs/installation) 

```
nvm install v16
```
```
npx create-next-app@latest --experimental-app
```
```
Need to install the following packages:
  create-next-app@13.3.1
Ok to proceed? (y) y
✔ What is your project named? … [blog-ai-app]
✔ Would you like to use TypeScript with this project? … No / [Yes]
✔ Would you like to use ESLint with this project? … No / [Yes]
✔ Would you like to use Tailwind CSS with this project? … No / [Yes]
✔ Would you like to use `src/` directory with this project? … [No] / Yes
✔ What import alias would you like configured? … @/*
```
```
npm run dev
```


```
cd blog-ai-app 
npm i @heroicons/react
```

[Tailwind](https://tailwindcss.com/docs/installation/using-postcss)
```
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init
```

## Extention
- [ES7+ React/Redux/React-Native snippets](https://marketplace.visualstudio.com/items?itemName=dsznajder.es7-react-js-snippets)
  - [snipet](https://github.com/ults-io/vscode-react-javascript-snippets/blob/HEAD/docs/Snippets.md)
    - rafce
      - tsrafce
- [Tailwind CSS IntelliSense](https://marketplace.visualstudio.com/items?itemName=bradlc.vscode-tailwindcss)
- [Tailwind Documentation](https://marketplace.visualstudio.com/items?itemName=alfredbirk.tailwind-documentation)

  - Mac: `cmd + ctrl + t`
    - Justify Content: `flex` `justify-between`
    - Padding: `px-10` `py-4`
    - Font Size: `text-sm` `text-3xl md:text-5xl`
    




# Dependencies

```
npm i @heroicons/react
npm i @tailwindcss/line-clamp
npm i -D @tailwindcss/typography
```


[Prisma]
[heroicons]
[TipTap]
[Typescript]
[Vercel]
[ChatGPT]

# PlanetScale CLI
[PlanetScale CLI](https://github.com/planetscale/cli#installation)
```
cd next-ai-blog-app
brew install planetscale/tap/pscale
```

```
cd blog-ai-app 
npx prisma init
```
## Prisma Extention
[Prisma](https://marketplace.visualstudio.com/items?itemName=Prisma.prisma)

## PlanetScale Database
[PlanetScale](https://planetscale.com/)
- PlanetScale is the world’s most advanced serverless MySQL platform
- create account - for Free account is only one Database
  - New database
    - Name: blog-ai-app
    - Region: Amazon Web Servicers us-east-1(Northern Virginia) <!-- 自分の現在地に近いところ -->
      - connect
        - copy and paste `Username` and `Password` to `.env` file
        - connect with: Node.js
        <!-- .gitignore に `.env` をアップデートしないように設定を忘れないこと // planetscale.com から Email にパスワード流出の警告がきて、パスワードがリセットされる -->
        - copy `DATABASE_URL` from `.env` tub and paste to `.env` <!-- 元からあった `DATABASE_URL` は不要 -->
          - Add `&&sslcert=/etc/ssl/cert.pem` end of `DATABASE_URL`
      - if connect issue
        - [Connecting to PlanetScale securely](https://planetscale.com/docs/concepts/secure-connections)
        - [Prisma Connecting to PlanetScale](https://github.com/prisma/prisma/issues/11246)

- Prisma
  - schema.prisma
    - datasource db
      - provider = "mysql"
      - relationMode = "prisma"
      - [Prisma schema](https://www.prisma.io/docs/concepts/components/prisma-schema)
      ```
      model Post {
        id        String   @id @default(cuid())
        createdAt DateTime @default(now())
        updatedAt DateTime @updatedAt
        title     String
        category  String
        content   String   @db.Text
        author    String
        image     String
        snippet   String   @db.Text
      }
      ```

- Push Prisma Database and verify at [planetscale.com](https://app.planetscale.com/)
  - Push Prisma Database
  ```
  cd blog-ai-app 
  npx prisma db push
  ```
  - planetscale.com
    - overview has `Tables 1`
    - type `show tables;` at console 
      - result
      ```
      1 row in (5.76 ms)
      Tables_in_blog-ai-app
      Post
      ```
    - type `SELECT * from Post;` at console 
      - result is blank table

- create Prisma Database
  - create file at /prisma/seed.ts
  - [Seeding your database](https://www.prisma.io/docs/guides/migrate/seed-database)
    ```
    cd blog-ai-app 
    npm install -D typescript ts-node @types/node
    ```
    - Add package.json
    ```
    "prisma": {
      "seed": "ts-node --compiler-options {\"module\":\"CommonJS\"} prisma/seed.ts"
    },
    ```
    - Update Prisma Database
    ```
    cd blog-ai-app 
    npx prisma db seed
    ```
      - verify at planetscale.com
        - type `show tables;` and `SELECT * from Post;` at console 
          - result
      - verify at Browser (Prisma API)
      ```
      cd blog-ai-app 
      npx prisma studio
      ```
        - result at `http://localhost:5555/`
          - click `post`

- OpenAI
  - [OpenAI](https://platform.openai.com/overview)
    - Manage Account
      - [API keys](https://platform.openai.com/account/api-keys)
        - `Create new secret key`, then Copy and Paste a API Key at ~~`.env`~~ `.env.local`

- OpenAI Node.js Library
[OpenAI Node.js Library](https://github.com/openai/openai-node)
```
npm install openai
```

- Nexi.js Deploy
[Static Export for App Router](https://nextjs.org/blog/next-13-3#static-export-for-app-router)
  - Add `output: 'export'` at `next.config.js`

- vercel.com Deploy
  - create account
    - connect git.hub `next-ai-blog-app`
      - Add `DATABASE_URL` and `OPENAI_API_KEY` at `Environment Variables`
        - `DATABASE_URL` is end part replace from `&&sslcert=/etc/ssl/cert.pem` to `&&sslcert=/etc/pki/tls/certs/ca-bundle.crt`

<!-- 
show tables;
SELECT * from Post;
 -->

- [Tiptap](https://tiptap.dev/)
  - For Page contents Edit form

  - [Tiptap Instration](https://tiptap.dev/installation/react#2-install-the-dependencies)
  ```
  npm install @tiptap/react @tiptap/pm @tiptap/starter-kit
  ```
  - Content.tsx
  ```
    const editor = useEditor({
    extensions: [
      StarterKit,
    ],
    content: '<p>Hello World!</p>',
  })
  ```



<!-- ///////////////////////////////////////////////////////////////////////////////////// -->
<!-- 
[Brilliant](https://brilliant.org/?utm_medium=sponsor&utm_source=youtube&utm_campaign=edrohmw_170423)


[nextjs installation](https://beta.nextjs.org/docs/installation)
[nextjs app roadmap](https://beta.nextjs.org/docs/app-directory-roadmap)
[nextjs new metadata](https://beta.nextjs.org/docs/api-reference/metadata)
[nextjs revalidation](https://beta.nextjs.org/docs/data-fetching/revalidating)
[nextjs revalidation not working](https://github.com/vercel/next.js/discussions/42290)
[nextjs config segments](https://beta.nextjs.org/docs/api-reference/segment-config#revalidate)
[nextjs font optimization](https://nextjs.org/docs/basic-features/font-optimization)
[nextjs limitations](https://vercel.com/docs/concepts/limits/overview)
[nextjs route nav](https://beta.nextjs.org/docs/routing/defining-routes)
[planetscale](https://planetscale.com/)
[planetscale cli](https://github.com/planetscale/cli#installation)
[planetscale certs](https://planetscale.com/docs/concepts/secure-connections)
[prisma/planetscale cert github](https://github.com/prisma/prisma/issues/11246)
[prisma schema docs](https://www.prisma.io/docs/concepts/components/prisma-schema)
[prisma seeding](https://www.prisma.io/docs/guides/migrate/seed-database)
[tiptap](https://tiptap.dev/)
[tiptap installation](https://tiptap.dev/installation/react)
[openai](https://platform.openai.com/)
[openai-node](https://github.com/openai/openai-node)
[openai-gpt4-signup](https://openai.com/waitlist/gpt-4-api) -->


<!-- ///////////////////////////////////////////////////////////////////////////////////// -->



<!-- 
This is a [Next.js](https://nextjs.org/) project bootstrapped with [`create-next-app`](https://github.com/vercel/next.js/tree/canary/packages/create-next-app).

## Getting Started

First, run the development server:

```bash
npm run dev
# or
yarn dev
# or
pnpm dev
```

Open [http://localhost:3000](http://localhost:3000) with your browser to see the result.

You can start editing the page by modifying `app/page.tsx`. The page auto-updates as you edit the file.

[API routes](https://nextjs.org/docs/api-routes/introduction) can be accessed on [http://localhost:3000/api/hello](http://localhost:3000/api/hello). This endpoint can be edited in `pages/api/hello.ts`.

The `pages/api` directory is mapped to `/api/*`. Files in this directory are treated as [API routes](https://nextjs.org/docs/api-routes/introduction) instead of React pages.

This project uses [`next/font`](https://nextjs.org/docs/basic-features/font-optimization) to automatically optimize and load Inter, a custom Google Font.

## Learn More

To learn more about Next.js, take a look at the following resources:

- [Next.js Documentation](https://nextjs.org/docs) - learn about Next.js features and API.
- [Learn Next.js](https://nextjs.org/learn) - an interactive Next.js tutorial.

You can check out [the Next.js GitHub repository](https://github.com/vercel/next.js/) - your feedback and contributions are welcome!

## Deploy on Vercel

The easiest way to deploy your Next.js app is to use the [Vercel Platform](https://vercel.com/new?utm_medium=default-template&filter=next.js&utm_source=create-next-app&utm_campaign=create-next-app-readme) from the creators of Next.js.

Check out our [Next.js deployment documentation](https://nextjs.org/docs/deployment) for more details. -->
