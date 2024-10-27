
## 📂 **1. Nama Modul: ChatTasker-Mobile**

- **Fungsi Utama**: Memberikan akses kepada pengguna melalui perangkat mobile untuk mengelola tugas dan berkomunikasi dengan chatbot.
- **Teknologi**:
  - *React Native* atau *Expo* untuk pengembangan aplikasi mobile
  - *Firebase* untuk penyimpanan data dan autentikasi
- **Repositori GitHub**: `ChatTasker-Mobile`

---

## 📘 **2. Deskripsi Modul**

Modul Mobile dirancang untuk memudahkan pengguna dalam mengelola tugas dari perangkat mobile mereka. Pengguna dapat melihat daftar tugas, memperbarui status tugas, serta berinteraksi dengan chatbot untuk mendapatkan informasi terkait tugas. Aplikasi ini akan terintegrasi dengan Firebase untuk menyimpan dan mengambil data tugas.

---

## 🚧 **3. Cara Kerja Modul**

### Alur Kerja

1. **Tampilan Daftar Tugas**:
   - Pengguna dapat melihat semua tugas yang telah dibuat, dengan status penyelesaian masing-masing.
2. **Manajemen Tugas**:
   - Pengguna dapat menambah, mengedit, atau menghapus tugas langsung dari aplikasi mobile.
3. **Interaksi dengan Chatbot**:
   - Pengguna dapat mengirim pesan ke chatbot dan menerima respons terkait tugas yang ada.
4. **Sinkronisasi Data**:
   - Data tugas akan secara otomatis disinkronkan dengan Firebase untuk memastikan informasi yang ditampilkan selalu up-to-date.

### Diagram Alur

1. **Pengguna Masuk** ➔ **Lihat Daftar Tugas** ➔ **Tambah/Edit Tugas** ➔ **Interaksi dengan Chatbot** ➔ **Notifikasi dan Pembaruan Status Tugas**

---

## 🛠️ **4. Tugas dan Fungsi Utama dalam Pengembangan**

### A. **Setup Proyek**

- **Tugas**: Mengatur proyek dengan menggunakan React Native atau Expo.
- **Langkah**:
  1. Inisialisasi proyek menggunakan Expo CLI atau React Native CLI.
  2. **Instalasi Dependensi**:
     ```bash
     # Jika menggunakan Expo
     npx create-expo-app ChatTasker-Mobile

     # Jika menggunakan React Native CLI
     npx react-native init ChatTasker-Mobile
     ```

### B. **Membangun Komponen Antarmuka**

- **Tugas**: Membuat komponen antarmuka untuk daftar tugas, formulir untuk menambah dan mengedit tugas, serta chat interface.
- **Langkah**:
  1. **Tampilan Daftar Tugas**:
     - Komponen yang menampilkan semua tugas dari database Firebase.
     - Menyediakan opsi untuk mengedit atau menghapus tugas.
  2. **Formulir Tugas**:
     - Komponen untuk menambah atau mengedit tugas.
     - Validasi input pengguna.
  3. **Chat Interface**:
     - Komponen untuk berinteraksi dengan chatbot.
     - Menampilkan pesan yang dikirim dan diterima.
- *Contoh Struktur Komponen*:
  ```
  src/
  ├── components/
  │   ├── TaskList.js
  │   ├── TaskForm.js
  │   ├── Chatbot.js
  ├── App.js
  └── firebaseConfig.js
  ```

### C. **Integrasi Firebase untuk Autentikasi dan Data**

- **Tugas**: Menghubungkan aplikasi mobile dengan Firebase untuk autentikasi pengguna dan akses data tugas.
- **Langkah**:

  1. Konfigurasi Firebase di proyek.
  2. Mengimplementasikan Firebase Authentication untuk memungkinkan pengguna masuk.

  - *Contoh Kode untuk Autentikasi*:
    ```javascript
    import firebase from 'firebase/app';
    import 'firebase/auth';

    const firebaseConfig = {
        apiKey: "YOUR_API_KEY",
        authDomain: "YOUR_PROJECT_ID.firebaseapp.com",
        // ...sisa konfigurasi
    };

    firebase.initializeApp(firebaseConfig);

    export const login = (email, password) => {
        return firebase.auth().signInWithEmailAndPassword(email, password);
    };

    export const logout = () => {
        return firebase.auth().signOut();
    };
    ```

### D. **Menghubungkan Aplikasi dengan Database**

- **Tugas**: Mengimplementasikan fungsi untuk mengakses dan memanipulasi data tugas di Firebase.
- **Langkah**:
  1. Menggunakan `firebase.database()` untuk melakukan operasi CRUD pada data tugas.
  2. Mengimplementasikan fungsi untuk menambah, memperbarui, dan menghapus tugas.
- *Contoh Kode untuk Mengakses Database*:
  ```javascript
  import firebase from 'firebase/app';
  import 'firebase/database';

  const database = firebase.database();

  export const fetchTasks = async () => {
      const snapshot = await database.ref('tasks').once('value');
      return snapshot.val();
  };

  export const createTask = async (taskData) => {
      const newTaskRef = database.ref('tasks').push();
      await newTaskRef.set(taskData);
      return newTaskRef.key;
  };
  ```

### E. **Mengimplementasikan Interaksi Chatbot**

- **Tugas**: Menghubungkan aplikasi mobile dengan chatbot untuk mengirim dan menerima pesan.
- **Langkah**:
  1. Buat fungsi untuk mengirim pesan ke API chatbot.
  2. Terima dan tampilkan respons dari chatbot di antarmuka pengguna.
- *Contoh Kode*:
  ```javascript
  const sendMessageToChatbot = async (message) => {
      const response = await fetch('http://localhost:5000/api/chat', {
          method: 'POST',
          headers: {
              'Content-Type': 'application/json',
          },
          body: JSON.stringify({ message }),
      });
      const data = await response.json();
      return data;
  };
  ```

---

## 🔗 **5. Struktur Proyek**

```
ChatTasker-Mobile/
├── src/
│   ├── components/
│   │   ├── TaskList.js
│   │   ├── TaskForm.js
│   │   ├── Chatbot.js
│   ├── App.js
│   ├── firebaseConfig.js
├── .env
├── package.json
└── README.md
```

---

## 🔒 **6. Keamanan dan Autentikasi**

- Gunakan Firebase Authentication untuk memastikan hanya pengguna yang terdaftar yang dapat mengakses data.
- Pastikan untuk menyimpan variabel lingkungan dengan aman dan tidak membagikannya di repositori publik.

---

## 📝 **7. Panduan Pengembangan**

1. **Clone Repositori**:

   ```bash
   git clone https://github.com/yourusername/ChatTasker-Mobile.git
   cd ChatTasker-Mobile
   ```
2. **Instalasi Dependensi**:

   ```bash
   npm install
   ```
3. **Menjalankan Aplikasi**:

   ```bash
   # Jika menggunakan Expo
   npx expo start

   # Jika menggunakan React Native CLI
   npx react-native run-android # Untuk Android
   npx react-native run-ios # Untuk iOS (di macOS)
   ```
4. **Pengujian Aplikasi**: Gunakan emulator atau perangkat nyata untuk menguji aplikasi dan memastikan semua fitur berfungsi.

---

## 📌 **8. Testing dan Pengujian**

- **Unit Testing**: Gunakan Jest atau Mocha untuk melakukan unit testing pada komponen React Native.
- **Integration Testing**: Uji integrasi antara mobile app dan backend API.
- **E2E Testing**: Uji end-to-end untuk memastikan seluruh alur aplikasi berjalan dengan baik.
