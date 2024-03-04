### Storage rules

- [rules](https://firebase.google.com/docs/storage/security/rules-conditions)

Granular operations

- read
  - get
  - list
- write
  - create
  - update
  - delete

``` cel
rules_version = '2';

function signed() {
  return request.auth != null;
}
function signedAndBelongs(userUid) {
  return signed() && request.auth.uid == userUid;
}
function validSize() {
  return request.resource.size < 1 * 1024 * 1024;
}
function validType() {
  return request.resource.contentType.matches('image/webp');
}
function valid() {
  return validSize() && validType();
}

service firebase.storage {
  match /b/{bucket}/o {
    match /{allPaths=**} {
      allow read;
      allow write: if false;
      
      match /users/{userUid}/temp/{imageUid} {
        allow read;
        allow write: if signedAndBelongs(userUid) && valid();
      }
      
      match /users/{userUid}/posts/{postUid}/{imageUid} {
        allow read;
        allow write: if signedAndBelongs(userUid);
      }
    }
  }
}
```

Разрешаем пользователю загружать файлы только в папку `/users/{userUid}/temp` и больше никуда, далее бекенд выполнит необходимое перемещние файлов согласно контексту вызова,  все остальное разрешено для чтения

Разрешаем пользователю работать с файлами в папке `/users/{userUid}/posts/{postUid}/{imageUid}` для удаления не используемых файлов при обновлении постов

Ожидаемые файлы только изображения формата **WebP** размерами до 1 мегабайта, эти файлы "чистовые" и должны быть подготовлены фронтом заранее, при загрузке указываются следющие заголовки:

``` json
{
  cacheControl: 'public, max-age=31536000, immutable',
  contentDisposition: 'attachment; filename=filename.webp',
  contentType: 'image/webp',
  customMetadata: {
    'Custom-Time': 'YYYY-MM-DD[T]HH:mm:ss[Z]'
  }
}
```
