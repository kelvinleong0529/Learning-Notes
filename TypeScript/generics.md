# **Generics**
- `generics` is the idea to allow type (integer, string, user-defined types etc) to be a parameter to methods, classes and interfaces
- `generics` can appear in functions, types, classes and interfaces
```javascript
function pickObjectKeys(obj, keys) {
  let result = {}
  for (const key of keys) {
    if (key in obj) {
      result[key] = obj[key]
    }
  }
  return result
}

const language = {
  name: "TypeScript",
  age: 8,
  extensions: ['ts', 'tsx']
}

const ageAndExtensions = pickObjectKeys(language, ['age', 'extensions'])
// {
//  age: 8,
//  extensions: ['ts', 'tsx']
// }
```
```typescript
function pickObjectKeys<T, K extends keyof T>(obj: T, keys: K[]) {
  let result = {} as Pick<T, K>
  for (const key of keys) {
    if (key in obj) {
      result[key] = obj[key]
    }
  }
  return result
}

const language = {
  name: "TypeScript",
  age: 8,
  extensions: ['ts', 'tsx']
}

const ageAndExtensions = pickObjectKeys(language, ['age', 'extensions'])
```
- `<T, K extends keyof T>` declares 2 params types for the function, where `K` is assigned a type that is the union of the keys in `T`
-  The `obj` function parameter is then set to whatever type T represents, and `keys` to an array of whatever type `K` represents.
-  Since `T` in the case of the `language` object sets `age` as a number and `extensions` as an array of strings, the variable `ageAndExtensions` will now be assigned the type of an object with properties `age: number` and `extensions: string[]`.