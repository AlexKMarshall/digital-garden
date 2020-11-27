# Validating Objects of Unknown Type

Even when using Typescript there are times when it is impossible to know for sure the type of an object. Generally this is when data enters our programme from outside.
Outside could be a file, a user input, data transmitted over http, data from a database.

To be sure the data is what we expect, we should parse it. Parsing will verify we have what we expect, and if we use Typescript, then we have type safety from this point on.

There are many libraries for validation:

- Joi: well established but doesn't play nicely with Typescript (we have to effectively double-enter our types)
- Yup: support for this built in with Formik but has limitations
- io-ts: made by the same people as fp-ts, haven't tried it
- Zod: Allows you to define the schema once then infer the type from it. Can create derived schemas using `pick` and `omit` commands

Zod has a `.safeParse` method that doesn't throw an exception, but returns a result that is either the parsed object, or an instance of `ZodValidationError`. It does this with a Typescript discriminated union. this is similar to fp-ts's `Either` type, but not exactly the same. 
So far I have been wrapping this call in a function that converts the result into an Either for compatibilty with fp-ts.

Usually this validation is strict, meaning validation will fail if there are additional fields on the object in question which aren't in the schema. This means validating something like an Express Request object is difficult, so validate just the `req.body` or similar. We have the same problem with Mongoose database objects, so use the `.toObject()` method.

#typescript #validation #functional-programming
