# Removing a Property from an Object in Typescript

You have a typed object, you would like a new object that is missing one of the props. But you'd like to maintain type safety

```typescript
function removeProp<T, K extends keyof T>(prop: K, obj T) {
  const {[prop]: _, ...rest}
  return rest
}
```

And could be curried

```typescript
function removeProp<T, K extends keyof T>(prop: K) {
  return (obj: T) => {
    const {[prop]: _, ...rest}
    return rest
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

const sanitizePerson = removeProp<Person, "passportNumber">("passportNumber")

const sanitizedPerson = sanitizePerson(somePerson)  // -> has type Pick<Person, "name" | "age">
```

Bit annoying that you have to specify the generic type K though. Not sure how to get around that. If you don't supply it, and just accept parameter `prop: keyof T` then you lose the resulting typing information
