## 声明 enum

```dart
enum Status {
  pending,
  completed,
  rejected,
}
```

> [!tip]
> `enum` 使用 `PascalCase` 命名, `enum values` 使用 `camelCase` 命名。

- [Enumerated types](https://dart.dev/language/enums)

## 使用

```dart
Status example = Status.pending;
print(example);
```

获取枚举值下标:

```dart
print(Status.pending.index); // 0
print(Status.completed.index); // 1
print(Status.rejected.index); // 2
```

获取枚举值:

```dart
print(Status.pending.name); // 'pending'
print(Status.pending.name == 'pending'); // true

print(Status.completed.name); // 'completed'
print(Status.rejected.name); // 'rejected'
```

> [!tip]
> 所有的枚举类都继承自 `Enum class`, 不可被 `subclass`、`implement` 或 `mixin`。

## Enhanced Enums

> [!caution]
> `Enhanced Enums` 于 `dart 2.17` 被引入, 因此使用此特性须确保 `pubspec.yaml` 中 `environment.sdk > = 2.17`, 否则会提示:
> > [!error]
> This requires the 'enhanced-enums' language feature to be enabled.

```dart
enum AuthException {
  invalidEmail('Invalid email'),
  emailAlreadyInUse('Email already in use'),
  weakPassword('Password is too weak'),
  wrongPassword('Wrong password');

  final String message;
  const AuthException(this.message);
}

AuthException exception = AuthException.wrongPassword;
print(exception.message); // Wrong password
```

```dart
enum StatusCode {
  badRequest(401, 'Bad request'),
  unauthorized(401, 'Unauthorized'),
  forbidden(403, 'Forbidden'),
  notFound(404, 'Not found'),
  internalServerError(500, 'Internal server error'),
  notImplemented(501, 'Not implemented');

  const StatusCode(this.code, this.description);
  final int code;
  final String description;

  @override
  String toString() => 'StatusCode($code, $description)';
}
```

- [How to Use Enhanced Enums with Members in Dart 2.17](https://codewithandrea.com/tips/dart-2.17-enums-with-members/)