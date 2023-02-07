#Design-Patterns #Singleton
# `TypeScript` Implement

> [!note]- Code
> ```ts
> class Singleton {
> 	private static instance: Singleton;
> 	private constructor() {}
> 	public static getInstance() {
> 		if (!Singleton.instance) {
> 			Singleton.instance = new Singleton();
> 		}
> 		return Singleton.instance;
> 	}
> }
> 
> const s1 = Singleton.getInstance();
> const s2 = Singleton.getInstance();
> console.log(s1 === s2);
> ```

```gist
cf9aff1884d586358c4157fab60d36c8
```

> [!note]
>如下代码
>```ts
>const s1 = new Singleton();
>```
>会报错
>`Constructor of class 'Singleton' is private and only accessible within the class declaration.ts(2673)`
>
>这是由于 `constructor` 之前的修饰词 `private` 所导致的:
>必须使类的**构造函数**只能在类的内部调用, 如此方可维护其单一性(**单例**)

- [Conceptual Example - TypeScript]([https://refactoring.guru/design-patterns/singleton/typescript/example](https://refactoring.guru/design-patterns/singleton/typescript/example#example-0--index-ts))

# `Dart` Implement

> [!note]- Code
> 
>```dart
>class Singleton {
>  static final Singleton _singleton = Singleton._internal();
>
 >  factory Singleton() {
>    return _singleton;
>  }
>
>  Singleton._internal();
>}
>
>void main() {
>  Singleton s1 = Singleton();
>  Singleton s2 = Singleton();
>  print(identical(s1, s2));
>  print(s1 == s2);
>}

```gist
21f710a8d3960f41f9ece27496298b55
```

- [how-do-you-build-a-singleton-in-dart - stackoverflow](https://stackoverflow.com/questions/12649573/how-do-you-build-a-singleton-in-dart)

# `Rust` Implement

- [Singleton in Rust - Safe Singleton](https://refactoring.guru/design-patterns/singleton/rust/example#example-0--safe-rs)
- [Singleton in Rust - Lazy Singleton](https://refactoring.guru/design-patterns/singleton/rust/example#example-1--lazy-rs)
- [Singleton in Rust - Singleton using Mutex](https://refactoring.guru/design-patterns/singleton/rust/example#example-2--mutex-rs)

# Reference

- [singelton - refactoring.guru](https://refactoring.guru/design-patterns/singleton)