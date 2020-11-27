# Removing a Property from an Object in Typescript

You have a typed object, you would like a new object that is missing one of the props. But you'd like to maintain type safety

```typescript
function removeProp<T, K extends keyof T>(prop: K, obj T) {
  const {[prop]: _, ...rest}
  return rest
}
```

To do the curried version is a little more work with generic types, as we don't know type T in advance, so we have to split up the generics, one for the outer function, one for the inner. See this https://github.com/microsoft/TypeScript/issues/14400#issuecomment-339127746

```typescript
function removeProp<K extends PropertyKey>(prop: K) {
  return <T extends {[prop in K]: any}>(obj: T) => {
    const {[prop]: _, ...rest} = obj;
    return rest;
  }
}
```

which would allow you to do something like

```typescript
type Person = {
  name: string;
  age: number;
  passportNumber: number
}

const sanitizePerson = removeProp("passportNumber")

const sanitizedPerson = sanitizePerson(somePerson)  // -> has type Pick<Person, "name" | "age">
```

And if you try to pass an object that doesn't have that prop to your partially applied function, then the compiler won't let you.
