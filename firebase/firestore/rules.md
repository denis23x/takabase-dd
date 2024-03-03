### Firestore rules

- [rules](https://firebase.google.com/docs/firestore/security/rules-conditions)

``` cel
rules_version = '2';

service cloud.firestore {
  match /databases/{database}/documents {
    function signed() {
      return request.auth != null;
    }
  	function signedAndBelongs(userUid) {
      return signed() && request.auth.uid == userUid;
    }

    match /users/{userUid} {
      allow read;
      allow create: if signed();
      allow update, delete: if signedAndBelongs(userUid);

      match /posts/{postUid} {
      	allow read;
        allow update, delete, create: if signedAndBelongs(userUid);
      }
    }
  }
}
```
