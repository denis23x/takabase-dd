### CORS configurations

- [guide](https://cloud.google.com/storage/docs/using-cors#command-line)

`cors.json`

``` json
[  
  {  
    "origin": [
      "https://takabase-dev.web.app", 
      "https://takabase-dev.firebaseapp.com"
    ], 
    "method": ["GET"],  
    "responseHeader": ["Content-Type"],  
    "maxAgeSeconds": 3600  
  }  
]
```

`gsutil cors set cors.json gs://takabase-dev.appspot.com`
