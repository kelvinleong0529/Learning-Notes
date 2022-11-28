# **Interfaces**
- typescript `interfaces` define the contracts within our code
- they provide explicit names for type checking
```typescript
interface Person {
    firstName: string;
    lastName: string;
}

function getFullName(person: Person) {
    return `${person.firstName} ${person.lastName}`;
}

let john = {
    firstName: 'John',
    lastName: 'Doe'
};

// prints 'John Doe'
console.log(getFullName(john));
```
```typescript
let jane = {
   firstName: 'Jane',
   middleName: 'K.'
   lastName: 'Doe',
   age: 22
};

let fullName = getFullName(jane);
// prints 'Jane Doe'
console.log(fullName);
```

## **Optional Parameters**
- an interface may have optional parameters
- use `?` at the end of property name in declaration to declare an optional property
```typescript
interface Person {
    firstName: string;
    middleName?: string;
    lastName: string;
}

function getFullName(person: Person) {
    if (person.middleName) {
        return `${person.firstName} ${person.middleName} ${person.lastName}`;
    }
    return `${person.firstName} ${person.lastName}`;
}
```

## **Read-only properties**
- we can use the `readonly` keyword before the name of the property
```typescript
interface Person {
    readonly ssn: string;
    firstName: string;
    lastName: string;    
}
// ssn property is READ-ONLY
```

## **Function types**
- `interfaces` also allow us to describe `function types`
- assign the interface to the function signature that contains the parameter list with types and returned types
```typescript
interface StringFormat {
    (str: string, isUpper: boolean): string
}

let format: StringFormat;

format = function (str: string, isUpper: boolean) {
    return isUpper ? str.toLocaleUpperCase() : str.toLocaleLowerCase();
};

console.log(format('hi', true));
```

## **Class Types**
- we can also use `interface` to define a contract between unrelated classes
```typescript
interface Json {
    toJSON(): string;
}

// declares a class that implements the 'Json' interface
// it implements the 'toJSON()` method of `Json` interface
class Person implements Json {
    constructor(private firstName: string,
        private lastName: string) {
    }
    toJson(): string {
        return JSON.stringify(this);
    }
}

let person = new Person('John', 'Doe');
console.log(person.toJson());
// output:
// {"firstName":"John","lastName":"Doe"}
```