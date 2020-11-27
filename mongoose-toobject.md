# Converting a Mongoose Document to a Javascript Object

We can call `.toObject()` on the document, this will change it to an object, and remove all the document methods like `.save()` etc.
It accepts an `options` object as a parameter. Some useful options could be

- `options.versionKey = false`: removes the `_v` prop from the object
- `options.transform = someFunction`: lets you run a function to transform the object, maybe removing props, or other changes

Alternatively, when doing `.find*()` methods, you can chain a `.lean()` method to it that will return plain objects. However, lean doesn't work on mutations, only plain reads.

#mongoose #backend
