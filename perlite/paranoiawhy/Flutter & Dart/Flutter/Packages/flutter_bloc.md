## context.read

- [context.read](https://bloclibrary.dev/#/flutterbloccoreconcepts?id=contextread)

`context.read<T>()` 等价于 `BlocProvider.of<T>(context)`:

```dart
// 1. context.read<T>()
context.read<CounterBloc>().add(CounterIncrementPressed());
// 2. BlocProvider.of<T>(context)
BlocProvider.of<CounterBloc>(context).add(CounterIncrementPressed());
```

## context.watch

- [context.watch](https://bloclibrary.dev/#/flutterbloccoreconcepts?id=contextwatch)

`context.watch<T>()` 等价于 `BlocProvider.of<T>(context, listen: true)`:
