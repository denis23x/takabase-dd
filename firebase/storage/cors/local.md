### CORS configurations

- [guide](https://cloud.google.com/storage/docs/using-cors#command-line)

`cors.json`

``` json
[  
  {  
    "origin": [
      "http://localhost:4200", 
      "http://localhost:4000"
    ],  
    "method": ["GET"],  
    "responseHeader": ["Content-Type"],  
    "maxAgeSeconds": 3600  
  }  
]
```

`gsutil cors set cors.json gs://takabase-local.appspot.com`
