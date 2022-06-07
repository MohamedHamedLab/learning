# Basics

## Strong typing
- Strong typing, or static typing as it is also known, means that when we create a variable, or define a parameter in a function, we specify what type it is.
  ```typescript
  var myString: string = `this is a string`;
  ```



## Basic types
- four common types, namely string, number, boolean, and array, and  any, null, never. 

```typescript
var myBoolean : boolean = true;
var myNumber : number = 1234;
var myStringArray : string[] = [`first`, `second`, `third`];
 ```


 ## The let keyword

```typescript
let index: number = 0;
if (index == 0) {
    let index: number = 2;
    console.log(`index = ${index}`);
}
console.log(`index = ${index}`);

// Result 
index = 2
index = 0
 ```

## Union types
- TypeScript allows us to express a type as a combination of two or more other types. These types are known as union types, and they use the pipe symbol ( | ) to list all of the types that will make up this new type.


```typescript
function printObject(obj: string | number) {
    console.log(`obj = ${obj}`);
}
printObject(1);
printObject("string value");
```

## Type guards
-  When working with union types, the compiler will still apply its strong typing rules to ensure type safety. 

```ts
function addWithUnion(
    arg1: string | number,
    arg2: string | number
) {
    return arg1 + arg2;
}

**Error**
 error TS2365: Operator '+' cannot be applied to types 'string | number' and 'string | number'

function addWithTypeGuard(
    arg1: string | number,
    arg2: string | number
) {
    if (typeof arg1 === "string") {
        // arg 1 is treated as a string
        console.log(`arg1 is of type string`);
        return arg1 + arg2;
    }
    if (typeof arg1 === "number" && typeof arg2 === "number") {
        // both are numbers
        console.log(`arg1 and arg2 are numbers`);
        return arg1 + arg2;
    }
    console.log(`default return treat both as strings`)
    return arg1.toString() + arg2.toString();
}

```

## Type aliases
- TypeScript introduces the concept of a type alias, where we can create a named type that can be used as a substitute for a type union.

```typescript
type StringOrNumber = string | number;
function addWithTypeAlias( 
    arg1: StringOrNumber,
    arg2: StringOrNumber
    ) {
    return arg1.toString() + arg2.toString();
}
```

**Explicit** describes something that is very clear and without vagueness or ambiguity.

 **Implicit** often functions as the opposite, referring to something that is understood, but not described clearly or directly
 
## Enums
- Enums are a special type whose concept is similar to other languages such as C#, C++, or Java, and provides the solution to the problem of special numbers, or special strings. Enums are used to define a human-readable name for a specific number or string.

```typescript
enum DoorState {
    Open,
    Closed
}
function checkDoorState(state: DoorState) {
    console.log(`enum value is : ${state}`);
    switch (state) {
        case DoorState.Open:
            console.log(`Door is open`);
            break;
        case DoorState.Closed:
            console.log(`Door is closed`);
            break;
    }
}
//  set the numerical value of an enum
enum DoorStateSpecificValues {
    Open = 3,
    Closed = 7,
    Unspecified = 256
}
// const enum
const enum DoorStateConst {
    Open = 10,
    Closed = 20
}
console.log(`const Closed = ${DoorStateConst.Open}`);

```