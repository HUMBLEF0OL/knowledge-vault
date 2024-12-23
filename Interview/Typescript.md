---
tags:
  - Interview-Prep
Date: 2024-10-12
Title: Typescript Interview Questions
References:
---

### **Basic Level Questions**

**Q1: What is TypeScript, and how is it different from JavaScript?**  
**A:**

- TypeScript is a superset of JavaScript that adds static typing, interfaces, and other features.
- It compiles down to plain JavaScript.
- Key difference: TypeScript provides type safety during development, catching errors before runtime.

---

**Q2: How do you declare variables in TypeScript with types?**  
**A:**  
You can explicitly define types using a colon `:`.

```typescript
let count: number = 10;
let name: string = "John";
let isAvailable: boolean = true;
```

---

**Q3: What are some key advantages of using TypeScript?**  
**A:**

- **Static Typing:** Reduces runtime errors.
- **Code Readability:** Improved clarity with type annotations.
- **Tooling Support:** Enhanced autocomplete and error detection in IDEs.
- **Compatibility:** Works with any JavaScript library or framework.

---

**Q4: Explain the `any` type in TypeScript.**  
**A:**

- The `any` type allows a variable to hold any type of value, bypassing static type checking.
- It's useful for scenarios where the type is dynamic or unknown.

```typescript
let variable: any = 42;
variable = "A string";
```

---

**Q5: What are enums in TypeScript?**  
**A:**  
Enums are a way to define named constants.

```typescript
enum Color {
  Red,
  Green,
  Blue,
}
let color: Color = Color.Green; // 1
```

---

### **Intermediate Level Questions**

**Q6: What is the difference between `interface` and `type`?**  
**A:**

- **`interface`**: Used to define the shape of an object or a class contract. Can be extended.
- **`type`**: Used for defining types like unions, intersections, and aliases. Cannot be extended.

```typescript
interface User {
  name: string;
}

type UserAlias = {
  name: string;
};
```

---

**Q7: What are TypeScript generics, and why are they useful?**  
**A:**  
Generics allow creating reusable, type-safe components.

```typescript
function identity<T>(arg: T): T {
  return arg;
}
const result = identity<number>(10);
```

---

**Q8: What are utility types in TypeScript?**  
**A:**  
Utility types are predefined types that simplify common type transformations:

- **`Partial<T>`**: Makes all properties optional.
- **`Required<T>`**: Makes all properties required.
- **`Readonly<T>`**: Makes all properties read-only.
- **`Pick<T, K>`**: Picks specific properties.

```typescript
interface User {
  id: number;
  name: string;
}
type ReadonlyUser = Readonly<User>;
```

---

**Q9: What are the differences between `unknown` and `any`?**  
**A:**

- **`unknown`**: Safer than `any`. You must perform type checks before using it.
- **`any`**: No restrictions or type checks.

```typescript
let value: unknown = "Hello";
if (typeof value === "string") {
  console.log(value.toUpperCase()); // Safe
}
```

---

**Q10: What is a tuple in TypeScript?**  
**A:**  
A tuple is a fixed-length array with specific types at each index.

```typescript
let tuple: [number, string] = [1, "hello"];
```

---

### **Advanced Level Questions**

**Q11: How does TypeScript handle function overloading?**  
**A:**  
TypeScript allows defining multiple function signatures for a single function.

```typescript
function add(a: number, b: number): number;
function add(a: string, b: string): string;
function add(a: any, b: any): any {
  return a + b;
}
```

---

**Q12: What is `never` in TypeScript?**  
**A:**

- Represents a value that never occurs.
- Typically used for functions that always throw errors or never return.

```typescript
function error(message: string): never {
  throw new Error(message);
}
```

---

**Q13: What are discriminated unions?**  
**A:**  
A union type with a common literal property for type narrowing.

```typescript
type Shape = { kind: "circle"; radius: number } | { kind: "square"; side: number };

function getArea(shape: Shape) {
  if (shape.kind === "circle") return Math.PI * shape.radius ** 2;
  if (shape.kind === "square") return shape.side ** 2;
}
```

---

**Q14: Explain `namespace` in TypeScript.**  
**A:**  
Namespaces group related code together, avoiding global scope pollution.

```typescript
namespace Utils {
  export function add(a: number, b: number): number {
    return a + b;
  }
}
console.log(Utils.add(2, 3));
```

---

**Q15: How does TypeScript support `abstract` classes?**  
**A:**  
Abstract classes provide a base structure for subclasses and cannot be instantiated.

```typescript
abstract class Animal {
  abstract sound(): void;
  move(): void {
    console.log("Moving...");
  }
}
class Dog extends Animal {
  sound(): void {
    console.log("Bark");
  }
}
```

---

**Q16: What are mapped types?**  
**A:**  
Mapped types transform existing types into new ones.

```typescript
type Optional<T> = {
  [K in keyof T]?: T[K];
};
interface User {
  id: number;
  name: string;
}
type OptionalUser = Optional<User>;
```

---

**Q17: How does TypeScript handle module resolution?**  
**A:**  
TypeScript resolves modules using `moduleResolution` settings (`node` or `classic`) based on file extensions and paths.

---

**Q18: What are declaration files in TypeScript?**  
**A:**  
Declaration files (`.d.ts`) provide type information for JavaScript libraries.

```typescript
declare module "library-name";
```

---

**Q19: What is `keyof` in TypeScript?**  
**A:**  
`keyof` is used to get a union of keys from a type.

```typescript
type User = { id: number; name: string };
type UserKeys = keyof User; // "id" | "name"
```

---

**Q20: Explain Type Guards in TypeScript.**  
**A:**  
Type guards narrow down types at runtime using conditionals.

```typescript
function isString(value: unknown): value is string {
  return typeof value === "string";
}
if (isString("hello")) {
  console.log("This is a string");
}
```

---

Would you like explanations or code examples for any specific question?