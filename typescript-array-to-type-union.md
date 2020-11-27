# Convert an array to a type union

```typescript
const validPets = ["cat", "dog", "horse"] as const
type Pet = typeof validPets[number]  // -> "cat" | "dog" | "horse"
```

The important bit is the `as const` otherwise Typescript thinks the array can contain any string.
