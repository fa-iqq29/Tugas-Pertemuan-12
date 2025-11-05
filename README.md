# 🧩 Tugas Pertemuan 12 – Penerapan GUI Database Berelasi

## 📘 Deskripsi Proyek

Repository ini berisi aplikasi GUI berbasis Java yang terhubung dengan database relasional melalui Java Persistence API (JPA). Aplikasi menampilkan data dari tabel-tabel yang memiliki relasi dan memungkinkan operasi CRUD. GUI memakai Swing dan menggunakan tabbed pane untuk membagi antar fungsi/modul.

---

## 🏗️ Fitur Utama

- Relasi antar tabel: Misalnya tabel Dosen memiliki relasi One → Many ke tabel MataKuliah.
- GUI dengan tabbed interface: Pengguna dapat berpindah antar tab untuk melihat/kelola entitas berbeda (misalnya: satu tab untuk Dosen, satu tab untuk MataKuliah).
- Operasi CRUD: Tambah, ubah, hapus, tampilkan data. Pada penghapusan, sistem mengecek relasi terlebih dahulu sebelum mengijinkan penghapusan untuk menjaga integritas.
- Validasi relasi: Jika suatu entitas (misalnya dosen) masih berelasi dengan entitas lain (mata kuliah), maka penghapusan ditolak.

---

## 🧠 Konsep Relasi (di JPA)

Contoh anotasi dalam entitas pada persistence:

<pre>java<br>
// Dosen.java
@OneToMany(mappedBy = "dosenPengajar", cascade = CascadeType.ALL)
private List<MataKuliah> mataKuliahs;

// MataKuliah.java
@ManyToOne
@JoinColumn(name = "id_dosen", referencedColumnName = "idDosen")
private Dosen dosenPengajar;
<br></pre>

Relasi ini memungkinkan aplikasi untuk mengecek dan menjaga integritas data (misalnya tidak menghapus dosen yang masih memiliki mata kuliah).

Selain itu, GUI menggunakan JTabbedPane supaya pengguna bisa:

- Berpindah antar tab “Dosen” dan “MataKuliah”.
- Masing-tab menampilkan panel sendiri dengan JTable, tombol CRUD, dsb. Referensi: tutorial Oracle tentang penggunaan JTabbedPane.

---

## ⚙️ Teknologi yang Digunakan

- Java (versi sesuai pengaturan proyek)
- JPA (dengan provider seperti Hibernate)
- Database relasional (contoh: MySQL)
- Swing GUI, menggunakan JTabbedPane untuk struktur tab
- IDE: NetBeans (atau lainnya yang mendukung Swing form builder)

---

⚠️ Catatan Penting

- Jika tab “Dosen” dipilih dan pengguna mencoba menghapus dosen yang masih memiliki mata kuliah, maka aplikasi akan menampilkan peringatan dan tidak melakukan penghapusan.
- Pastikan tabel database membuat foreign key yang relevan, misalnya:
<pre>sql<br>
CREATE TABLE Dosen (
    id_dosen CHAR(4) PRIMARY KEY,
    nama_dosen VARCHAR(100),
    nip VARCHAR(50),
    email VARCHAR(100)
);

CREATE TABLE MataKuliah (
    id_matkul CHAR(9) PRIMARY KEY,
    nama_matkul VARCHAR(100),
    sks_matkul INT,
    dosen_pengajar CHAR(4),
    FOREIGN KEY (dosen_pengajar) REFERENCES Dosen(id_dosen)
);
<br></pre>

---

## ✍️ Penulis

Faiq

Mahasiswa Sistem Informasi

Semester 3

Universitas Islam Negeri Sunan Ampel Surabaya
