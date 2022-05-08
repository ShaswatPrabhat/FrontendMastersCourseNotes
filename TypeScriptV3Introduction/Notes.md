* Course notes: https://www.typescript-training.com/course/fundamentals-v3
* Typescript is a syntactic superset of JavaScript
* It contains of the Language itself, the Languager server which integrates with IDE's to enable autocomplete and the compiler
* Allows to add intent to the code as an author
* Errors move from runtime to compile time like internal contracts
* One of the core principles is that code in Javascript should be interoperable with TypeScript
* Normally tsc will create the typescript files along with JS files. The `outDir` entity in `tsconfig` helps to have all the outputs in one directory.
* Everything in `compilerOptions` can be passed to the `tsc` command as command line arguments.
* If we need to target several versions then typically we can get TS to output in ES6 and then use babel to transpile to an older version for support
* A good way to think of TS files:
    - .ts files contain both type information and code that runs
    - .js files contain only code that runs
    - .d.ts files contain only type information
* Node expects CommonsJs modules stil
* Adding a `module` in `tsconfig` adds this functionality of emitting CommonJS
* A variable is born with the type it was initialized it
* It is hard to make that type more general after initialization
* Literal types are initialized with `const` 
* It will forever be pointing to the same location
* hence the type is the value for a `const`
* TypeScript tries to always make the most specific assumption that it can without risking getting in the way.
* Hence let declarations are more lax
* any is the most flexible type in TS
* Types are assignd to variables when those are born hence there is an any type for late intialized variables
* that is where a type annotation comes in picture. if we say `let endtime:Date` we are are telling TS the type of data the varibale will hold in the future
* `any` kind of breaks the typedness of the code so we want to use it as sparingly as possible
* With the prefernce of problems surfacing where we declare the function vs where we use the function
* If we specify it at function declaration, we would have stated the contract and hence reduces noise
* Typescript is not a replacement for Tests just for Types, nothing to do with behavour
* We can very  well do this for a shape or object composite type:
```typescript
let car: {
  make: string
  model: string
  year: number
}
```
* For optional properties we can specify`?:` operator ``` chargeVoltage?:number```
* We can have code like a typeguard which TS compiler will understand and eliminate a specific type. Say:
```typescript
if (typeof car.chargeVoltage !== "undefined")
    str += `// ${car.chargeVoltage}v`
```
    in the above the type of car.chargeVoltage will automatically be number and then checks based on that
* Read TS errors from bottom up
* Tuples can be treated as an array as of TS 4.3
* Push pop etc are all allowed and throw no errors.
* So a push or pop is not going to change the type of the operand in TS yet
* Compilation target to JS is a major feature for a lot of languages
* Mainly other languages keep JS as a build target and implement run time type checking.
* Type checking is evaluates the question of compatibilty and type equivalence
* Mostly happens during assignemt and passing values to a function
* Happens on return, whether the type I am returning from a function the same as the one which I have declared
* Type systems is either static vs dynamic, depending on whether the type checking happening at compile time vs run time.
* TS is statically typed
* Nominal type systems are all about NAMES
* Eveything is about the name of your class and that becomes a cutom type
* The above wont fit JS code
* Structural type system  are all about strucutre and shape
* TS is Structurally typed
* The name of the obect plays no role in type equivalence checking. Only the shape
* Duck typing kind of dynamic typing similar to Structural typing
* Union and intersection types: Kind of logical operators AND and OR
* 