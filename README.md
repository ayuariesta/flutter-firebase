# flutter-firebase
Praktikum Flutter Firebase

## Get the sample code
![Screenshot step_02](images/01.png)

## Create a Firebase project
![Screenshot step_02](images/02.png)

## Enable email sign-in for Firebase Authentication
![Screenshot step_02](images/06.png)

## Enable Cloud Firestore
![Screenshot step_02](images/09.png)

## Configure dependencies
```
flutter pub add firebase_core 
```
firebase_core adalah kode umum yang diperlukan untuk semua plugin Firebase Flutter.

```
flutter pub add firebase_auth
```
firebase_auth memungkinkan integrasi dengan kemampuan Otentikasi Firebase.
```
flutter pub add cloud_firestore
```
cloud_firestore memungkinkan akses ke penyimpanan data Cloud Firestore.
```
flutter pub add provider
```
menggunakan paket provider yang akan memungkinkan pemisahan logika bisnis dari logika tampilan.

## Install Flutterfire
```
dart pub global activate flutterfire_cli
```

## Configure apps
```
flutterfire configure
```

## Add user sign-in (RSVP)
![Screenshot step_02](images/13.png)

## Login menggunakan email
![Screenshot step_02](images/14.png)

## Create Account
![Screenshot step_02](images/15.png)

## Tampilan saat sudah login
![Screenshot step_02](images/16.png)

## Write messages to Cloud Firestore
![Screenshot step_02](images/17.png)

## Tampilan Cloud Firestore saat user mengirim pesan
![Screenshot step_02](images/22.png)

## Read messages
![Screenshot step_02](images/20.png)

## Add validation rules
```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /guestbook/{entry} {
      allow read: if request.auth.uid != null;
      allow write:
      if request.auth.uid == request.resource.data.userId
          && "name" in request.resource.data
          && "text" in request.resource.data
          && "timestamp" in request.resource.data;
    }
  }
}
```

## Status RSVP Pengguna
![Screenshot step_02](images/21.png)

## Add validation rules
```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /guestbook/{entry} {
      allow read: if request.auth.uid != null;
      allow write:
      if request.auth.uid == request.resource.data.userId
          && "name" in request.resource.data
          && "text" in request.resource.data
          && "timestamp" in request.resource.data;
    }
    match /attendees/{userId} {
      allow read: if true;
      allow write: if request.auth.uid == userId
          && "attending" in request.resource.data;

    }
  }
}
```
