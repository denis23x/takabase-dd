### Object Lifecycle Management

- [guide](https://cloud.google.com/storage/docs/lifecycle)
- [console](https://console.cloud.google.com/storage/browser/takabase-local.appspot.com)

~~Предыдущие правила не сработали (вероятно кривой префикс)~~

> 1. Изображения с префиксом `/temp`
> 2. Изображения чей **Custom-Time** устарел на 1 день

~~Сейчас установлено (наблюдаю)~~

> 1. Изображения с префиксом `/users/{userUid}/temp`
> 2. Изображения чей **Age** устарел на 1 день

Сейчас установлено (наблюдаю)

> 1. Изображения с префиксом `/users/{userUid}/temp`
> 2. Изображения с префиксом `/users/{userUid}/temp/`
> 3. Изображения с префиксом `/users/**/temp`
> 4. Изображения с префиксом `/users/**/temp/`
> 5. Изображения чей **Age** устарел на 1 день
