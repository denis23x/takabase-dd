### Описание привязки загружаемых изображений в Markdown

Изображения загружаемые через **Cropper** по умолчанию загружаются в **Storage** по адресу `users/{userUid}/temp`

> Изображения загружаются с специальным заголовком Custom-Time в котором указано время начала загрузки файла, внутри Google Cloud Storage настроен сервис Object Life Cycle имеющий 2 правила:
> 1. Изображения с префиксом `/temp` не важно расположение файла, правило аффектит всю корзину, любая вложенность
> 2. Изображения чей Custom-Time устарел на 1 день
>
> При совпадении обоих правил, файл безвозвратно будет удален

При создании нового поста, создается пустой документ в **Firestore** по адресу `users/{userUid}/posts/{postUid}` полученный `postUid` далее отправляется на бекенд как поле `firebaseUid`

Бекенд парсит загружаемый **Markdown** на наличие изображений с ссылками на `users/{userUid}/temp` при нахождении которых переносит изображения в **Storage** по адресу `users/{userUid}/posts/{postUid}` где `postUid` это `firebaseUid`

После переноса изображений бекенд обновляет ссылки в **Markdown** и создает запись в БД, `firebaseUid` тоже сохраняется, отправляется ответ на фронтенд

> Изображения переносит именно бекенд, потому что фронтовые пакеты Firebase не обладаюст достаточным функционалом, на бекенде используется пакет Google Cloud Storage

Фронтенд парсит полученный **Markdown** на наличие изображений с ссылками на `users/{userUid}/posts/{postUid}` и обновляет пустой документ **Firestore** записывая туда `postId` полученный в ответе сервера, а так же массив ссылок изображений

Таким образом в обоих базах данных существуют записи с постом и идентификаторами друг друга, база бекенда основная, **Firestore** вспомогательная

### Описание обновления привязки загружаемых изображений в Markdown

Бекенд обновляет запись в своей БД аналогично созданию, то есть происходит тот же сценарий с поиском в **Markdown** временных изображений и перенос их на постоянное месторасположение

Фронтенд получет ответ от бекенда и формирует 2 списка для вычисления изменений:

1. *Фактический (в текстовом выражении)* - фронтенд парсит полученный **Markdown** на наличие изображений с ссылками на `users/{userUid}/posts/{postUid}`
2. *Фактический (в файловом выражении)* - фронтенд запрашивает список файлов в **Storage** по адресу `users/{userUid}/posts/{postUid}`

Списки сравниваются следующим образом, пробегаем по списку полученных изображений из **Storage** и ищем каждое такое изображение в **Markdown** если изображение не найдено, следовательно файл существует в **Storage** но в **Markdown** на него больше никто не ссылается, такой файл добавляется в список на удаление, фронтенд удаляет не используемые файлы и обновляет список изображений в документе в **Firestore**