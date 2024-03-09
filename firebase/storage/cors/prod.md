### CORS configurations

- [guide](https://cloud.google.com/storage/docs/using-cors#command-line)

`cors.json`

``` json
[  
  {  
    "origin": [
      "https://takabase-prod.web.app",
      "https://takabase-prod.firebaseapp.com",
      "https://takabase.com"
    ], 
    "method": ["GET"],  
    "responseHeader": ["Content-Type"],  
    "maxAgeSeconds": 3600  
  }  
]
```

`gsutil cors set cors.json gs://takabase-prod.appspot.com`
