# Working with Express and Typescript

It can be a bit of a pain, mainly because Express passes around mutable `Request` and `Response` objects that have a lot of properties and can be hard to mock.
If you use `express-jwt` then this creates a `.user` prop on the reuest, but the base types from `@types/express` don't have this user prop, so you can't access it without Typescript complaining.
You might think `@types/express-jwt` would have it, but nope.

Instead, we need to merge the declaration of the `Request` object.

Create a folder at the root of the project called `@types/express` and in there create an `index.d.ts` containing

```typescript
// eslint-disable-next-line no-unused-vars
declare namespace Express {
  export interface Request {
    user?: {
      sub: string;  // this is the user ID coming from auth0
      // any other properties of the user object you need
    };
  }
}
```

Now we need Typescript to recognise this.

In tsconfig.json we need the following. The ordering in the `typeRoots` array is important - our declarations must come before the ones in `node_modules`

```json
{
  "compilerOptions": {
    "typeRoots": ["@types", "node_modules/@types"],
  },
  "include": ["src/**/*", "@types"],
}
```

This still won't play nicely with ts-node/nodemon so we need to add a `--files` flag to our nodemon script:

```
nodemon -x ts-node --files
```

#typescript #express #backend
