### Application Default Credentials

- [guide](https://cloud.google.com/docs/authentication/application-default-credentials)

Для продолжения необходимо [установить инструменты](install.md)

Повторить для всех окружений в публичных окружениях использовать **Secret Manager**

Необходимо создать файл с учетными данными по умолчанию и указать его в переменных окружения бекенда

`.gcp-adc.json`

```json
{
  "account": "",
  "client_id": "764086051850-6qr4p6gpi6hn506pt8ejuq83di341hur.apps.googleusercontent.com",
  "client_secret": "d-FL95Q19q7MQmFpd7hHD0Ty",
  "quota_project_id": "takabase-local",
  "refresh_token": "1//0gmFfnRCP9-UwCgYIARAAGBASNwF-L9IrdnRXQ1ny0siB6wy8LuqHxa5KL_pXsyKGeVNjD_QOX9GjTLedGoTOXtH5iS2Nen0Hj_U",
  "type": "authorized_user",
  "universe_domain": "googleapis.com"
}
```

`.env`

```dotenv
GOOGLE_APPLICATION_CREDENTIALS=.gcp-adc.json
```
