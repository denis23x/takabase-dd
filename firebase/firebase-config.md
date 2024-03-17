### Firebase Config

- [guide](https://firebase.google.com/docs/admin/setup)

Повторить для всех окружений в публичных окружениях использовать **Secret Manager**

Необходимо создать файл с учетными данными по умолчанию и указать его в переменных окружения бекенда

`.gcp-firebase.json`

```json
{
  "apiKey": "AIzaSyBjYjnCQeQzGPePjsDqgU_EpOqRyF0YadM",
  "authDomain": "takabase-local.firebaseapp.com",
  "projectId": "takabase-local",
  "storageBucket": "takabase-local.appspot.com",
  "messagingSenderId": "804966843833",
  "appId": "1:804966843833:web:0fda27de913151deb36268"
}
```

`.env`

```dotenv
FIREBASE_CONFIG=.gcp-firebase.json
```
