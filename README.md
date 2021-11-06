# Project

## Some prerequisite
1. Setup account in https://supabase.io/
2. Knowledge of Reactjs, GraphQL
3. Installed VS code

## Structure of this demo
1. Build backend API with Headless CMS (keystonejs)
2. Build client web app with next.js, prisma and apollo client

## Setup backend API project

Run in terminal
```
npx create-keystone-app
```

Give name to project.
```
propel-demo-app
```
![Screen Shot 2021-11-06 at 10 06 35 am](https://user-images.githubusercontent.com/1040210/140590810-9324c0a7-3bca-4ac0-b601-38360f0f6ee4.png)

Run
```
cd propel-demo-app && code .
```

## Upgrade DB settings to postgresql
1. Go to https://supabase.io/ and create a new project
![Screen Shot 2021-11-06 at 11 10 50 am](https://user-images.githubusercontent.com/1040210/140590993-b9096d2a-a847-482b-b3f6-e6eccba67a42.png)
2. Go to Settings page, click Database and copy `connectionString`. 
3. Rename `postgresql` to `postgres` at the start of connection string, and replace `[YOUR-PASSWORD]` to your password. 
4. End result should be: `postgresql://postgres:PropelDemoAppDb@db.akerbvropljqboyamhou.supabase.co:5432/postgres`
5. Go back to project settings and find `keystone.js` file and modify connection string

```
db: {
    provider: 'postgresql',
    url: 'postgresql://postgres:PropelDemoAppDb@db.akerbvropljqboyamhou.supabase.co:5432/postgres',
    onConnect: async context => { /* ... */ },
    // Optional advanced configuration
    enableLogging: true,
    useMigrations: true,
    idField: { kind: 'uuid' },
  },
```
6. Run `npm run dev` or `yarn dev`
7. Name migration `init migration`
    ![Screen Shot 2021-11-06 at 11 24 25 am](https://user-images.githubusercontent.com/1040210/140591398-18ddc930-9321-4ee5-a77f-471c6e356c6a.png)

## Open Keystone.js
1. Open URL: `http://localhost:3000/` 
2. Setup Admin account in CMS. Password `PropelDemo`
![Screen Shot 2021-11-06 at 11 30 04 am](https://user-images.githubusercontent.com/1040210/140591573-1a2c5f43-5390-43c5-ab2f-1421d6165f18.png)
3. Create first post.
![Screen Shot 2021-11-06 at 11 34 00 am](https://user-images.githubusercontent.com/1040210/140591712-0b166ff8-a48b-4f7b-9ff8-02f366fe1256.png)


### Adding a frontend

As a Headless CMS, Keystone can be used with any frontend that uses GraphQL. It provides a GraphQL endpoint you can write queries against at `/api/graphql` (by default [http://localhost:3000/api/graphql](http://localhost:3000/api/graphql)). At Thinkmill, we tend to use [Next.js](https://nextjs.org/) and [Apollo GraphQL](https://www.apollographql.com/docs/react/get-started/) as our frontend and way to write queries, but if you have your own favourite, feel free to use it.

A walkthrough on how to do this is forthcoming, but in the meantime our [todo example](https://github.com/keystonejs/keystone-react-todo-demo) shows a Keystone set up with a frontend. For a more full example, you can also look at an example app we built for [Prisma Day 2021](https://github.com/keystonejs/prisma-day-2021-workshop)

### Embedding Keystone in a Next.js frontend

While Keystone works as a standalone app, you can embed your Keystone app into a [Next.js](https://nextjs.org/) app. This is quite a different setup to the starter, and we recommend checking out our walkthrough for that [here](https://keystonejs.com/docs/walkthroughs/embedded-mode-with-sqlite-nextjs#how-to-embed-keystone-sq-lite-in-a-next-js-app).
