# BambangShop Receiver App
Tutorial and Example for Advanced Programming 2024 - Faculty of Computer Science, Universitas Indonesia

---

## About this Project
In this repository, we have provided you a REST (REpresentational State Transfer) API project using Rocket web framework.

This project consists of four modules:
1.  `controller`: this module contains handler functions used to receive request and send responses.
    In Model-View-Controller (MVC) pattern, this is the Controller part.
2.  `model`: this module contains structs that serve as data containers.
    In MVC pattern, this is the Model part.
3.  `service`: this module contains structs with business logic methods.
    In MVC pattern, this is also the Model part.
4.  `repository`: this module contains structs that serve as databases.
    You can use methods of the struct to get list of objects, or operating an object (create, read, update, delete).

This repository provides a Rocket web framework skeleton that you can work with.

As this is an Observer Design Pattern tutorial repository, you need to implement a feature: `Notification`.
This feature will receive notifications of creation, promotion, and deletion of a product, when this receiver instance is subscribed to a certain product type.
The notification will be sent using HTTP POST request, so you need to make the receiver endpoint in this project.

## API Documentations

You can download the Postman Collection JSON here: https://ristek.link/AdvProgWeek7Postman

After you download the Postman Collection, you can try the endpoints inside "BambangShop Receiver" folder.

Postman is an installable client that you can use to test web endpoints using HTTP request.
You can also make automated functional testing scripts for REST API projects using this client.
You can install Postman via this website: https://www.postman.com/downloads/

## How to Run in Development Environment
1.  Set up environment variables first by creating `.env` file.
    Here is the example of `.env` file:
    ```bash
    ROCKET_PORT=8001
    APP_INSTANCE_ROOT_URL=http://localhost:${ROCKET_PORT}
    APP_PUBLISHER_ROOT_URL=http://localhost:8000
    APP_INSTANCE_NAME=Safira Sudrajat
    ```
    Here are the details of each environment variable:
    | variable                | type   | description                                                     |
    |-------------------------|--------|-----------------------------------------------------------------|
    | ROCKET_PORT             | string | Port number that will be listened by this receiver instance.    |
    | APP_INSTANCE_ROOT_URL   | string | URL address where this receiver instance can be accessed.       |
    | APP_PUUBLISHER_ROOT_URL | string | URL address where the publisher instance can be accessed.       |
    | APP_INSTANCE_NAME       | string | Name of this receiver instance, will be shown on notifications. |
2.  Use `cargo run` to run this app.
    (You might want to use `cargo check` if you only need to verify your work without running the app.)
3.  To simulate multiple instances of BambangShop Receiver (as the tutorial mandates you to do so),
    you can open new terminal, then edit `ROCKET_PORT` in `.env` file, then execute another `cargo run`.

    For example, if you want to run 3 (three) instances of BambangShop Receiver at port `8001`, `8002`, and `8003`, you can do these steps:
    -   Edit `ROCKET_PORT` in `.env` to `8001`, then execute `cargo run`.
    -   Open new terminal, edit `ROCKET_PORT` in `.env` to `8002`, then execute `cargo run`.
    -   Open another new terminal, edit `ROCKET_PORT` in `.env` to `8003`, then execute `cargo run`.

## Mandatory Checklists (Subscriber)
-   [x] Clone https://gitlab.com/ichlaffterlalu/bambangshop-receiver to a new repository.
-   **STAGE 1: Implement models and repositories**
    -   [x] Commit: `Create Notification model struct.`
    -   [x] Commit: `Create SubscriberRequest model struct.`
    -   [x] Commit: `Create Notification database and Notification repository struct skeleton.`
    -   [x] Commit: `Implement add function in Notification repository.`
    -   [x] Commit: `Implement list_all_as_string function in Notification repository.`
    -   [x] Write answers of your learning module's "Reflection Subscriber-1" questions in this README.
-   **STAGE 3: Implement services and controllers**
    -   [x] Commit: `Create Notification service struct skeleton.`
    -   [x] Commit: `Implement subscribe function in Notification service.`
    -   [x] Commit: `Implement subscribe function in Notification controller.`
    -   [x] Commit: `Implement unsubscribe function in Notification service.`
    -   [x] Commit: `Implement unsubscribe function in Notification controller.`
    -   [x] Commit: `Implement receive_notification function in Notification service.`
    -   [x] Commit: `Implement receive function in Notification controller.`
    -   [x] Commit: `Implement list_messages function in Notification service.`
    -   [x] Commit: `Implement list function in Notification controller.`
    -   [x] Write answers of your learning module's "Reflection Subscriber-2" questions in this README.

## Your Reflections
This is the place for you to write reflections:

### Mandatory (Subscriber) Reflections

#### Reflection Subscriber-1
1. Dalam tutorial ini, kita menggunakan RwLock<> untuk menyinkronkan penggunaan Vec of Notifications. Hal ini diperlukan karena kita ingin memastikan bahwa operasi penambahan dan penghapusan notifikasi dari Vec dapat dilakukan secara aman oleh beberapa thread secara bersamaan. RwLock memungkinkan akses bersamaan untuk pembacaan (read) oleh beberapa thread, namun hanya satu thread yang dapat menulis (write) pada satu waktu. Penggunaan RwLock<> lebih cocok untuk kasus ini daripada Mutex<>, karena Mutex<> hanya mengizinkan satu thread untuk mengakses data pada satu waktu, baik untuk membaca maupun menulis.

2. Dalam tutorial ini, kita menggunakan library eksternal lazy_static untuk mendefinisikan Vec dan DashMap sebagai variabel "static". Berbeda dengan Java, di mana kita dapat memperbarui konten dari variabel statis melalui sebuah fungsi statis, Rust tidak mengizinkan hal tersebut. Hal ini disebabkan karena Rust memiliki konsep kepemilikan yang ketat dan menekankan pada keamanan konkurensi. Rust melarang mutasi langsung pada variabel statis karena dapat menyebabkan kondisi race dan data races yang tidak terduga, yang dapat mengakibatkan perilaku program yang tidak dapat diprediksi. Oleh karena itu, variabel statis dalam Rust secara default bersifat tidak dapat diubah (immutable), yang membuat Rust menjadi bahasa yang terkenal karena keamanan dan keandalannya dalam pemrograman konkurensi dibandingkan dengan Java.

#### Reflection Subscriber-2
1. Saya telah menjelajahi bagian-bagian di luar langkah-langkah dalam tutorial, seperti src/lib.rs. Di dalam `lib.rs`, terdapat dependensi dan konfigurasi awal. Selain itu, terdapat inisialisasi dari APP_CONFIG dan REQUEST_CLIENT yang digunakan di seluruh implementasi kode. Berkas ini bertugas untuk mendefinisikan komponen-komponen yang diperlukan oleh aplikasi. Sedangkan `Cargo.toml` adalah berkas konfigurasi utama untuk proyek Rust. Ini berperan sebagai pusat manajemen dependensi, konfigurasi proyek, dan mendefinisikan metadata proyek. Kedua berkas ini memegang peranan penting dalam menyiapkan dan memelihara proyek Rust, memastikan konsistensi dan kelolaan selama proses pengembangan.

2. Pola Observer memudahkan penambahan subscriber tambahan ke dalam sistem notifikasi, membuat arsitektur kode lebih fleksibel dan dapat berkembang. Hal ini karena pola Observer memisahkan antara penerbit dan pengamatnya. Memunculkan lebih dari satu instansi dari aplikasi utama masih cukup mudah dilakukan karena ada pemrosesan paralel untuk notifikasi, membuat kode lebih efisien.

3. Saya telah mencoba membuat tes sendiri dan meningkatkan dokumentasi pada koleksi Postman saya (menambahkan deskripsi yang jelas untuk setiap permintaan). Walaupun saya belum yakin apakah itu sudah benar, saya yakin bahwa fitur ini sangat berguna untuk pekerjaan saya. Ini membantu melakukan pengujian otomatis saat menguji respons server.