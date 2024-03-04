### Firestore rules

- [rules](https://firebase.google.com/docs/firestore/security/rules-conditions)

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

service cloud.firestore {
  match /databases/{database}/documents {
    match /{allDocuments=**} {
      allow read;
      allow write: if false;
      
      match /users/{userUid} {
        allow read;
        allow write: if signedAndBelongs(userUid);

        match /posts/{postUid} {
          allow read;
          allow write: if signedAndBelongs(userUid);
        }
      }
    }
  }
}
```
