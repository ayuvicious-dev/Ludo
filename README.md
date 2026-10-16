# Ludo

Game Ludo klasik (PWA) dengan login Firebase Authentication dan penyimpanan Cloud Firestore.

## Fitur
- Login email/kata sandi dan Google
- 2 sampai 4 pemain, bisa melawan bot atau bergantian dengan teman di satu perangkat
- Simpan dan lanjutkan game dari perangkat mana pun
- Statistik menang dan papan peringkat
- Bisa dipasang di layar utama (PWA)

## Setup Firebase (project `ludo-c1094`)
1. Authentication > Sign-in method: aktifkan **Email/Password** dan **Google**.
2. Authentication > Settings > Authorized domains: tambahkan `USERNAME.github.io`.
3. Firestore Database > Rules: tempel isi berikut lalu **Publish**.

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /users/{uid} {
      allow read: if request.auth != null;
      allow write: if request.auth != null && request.auth.uid == uid;
      match /private/{doc} {
        allow read, write: if request.auth != null && request.auth.uid == uid;
      }
    }
  }
}
```

## Deploy
Upload semua file ke repository GitHub, lalu Settings > Pages > Deploy from branch (`main`, folder `/root`).
