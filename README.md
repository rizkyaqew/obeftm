# OBE FTM Unjani

Dokumentasi awal struktur endpoint dan model data untuk aplikasi **OBE FTM Unjani**.  
Dokumen ini mencakup entitas master sampai dengan **MataKuliah**.

---

## Daftar Isi

- [Konvensi Endpoint](#konvensi-endpoint)
- [Universitas](#universitas)
- [Fakultas](#fakultas)
- [Prodi](#prodi)
- [TahunAjaran](#tahunajaran)
- [Kurikulum](#kurikulum)
- [ProfilLulusan](#profillulusan)
- [MasterCPL](#mastercpl)
- [MataKuliah](#matakuliah)

---

## Konvensi Endpoint

Struktur endpoint umum yang digunakan adalah sebagai berikut:

### 1. Akses sebuah entitas
```http
GET /api/v1/[nama_entitas]/[id]
```

### 2. List semua entitas
```http
GET /api/v1/list/[nama_entitas]/[id_parent]
```

> **Catatan:** khusus entitas **Universitas**, parameter `[id_parent]` tidak diperlukan.

### 3. Insert entitas baru
```http
POST /api/v1/add/[nama_entitas]
```

### 4. Update sebuah entitas
```http
POST /api/v1/edit/[nama_entitas]/[id]
```

### 5. Nonaktifkan sebuah entitas
```http
DELETE /api/v1/[nama_entitas]/[id]
```

### 6. Aktifkan kembali sebuah entitas
```http
PATCH /api/v1/[nama_entitas]/[id]
```

---

## Universitas

Entitas **Universitas** adalah level tertinggi dalam struktur data.  
Satu universitas dapat menaungi banyak fakultas.

### Endpoint

#### Ambil data universitas berdasarkan ID
```http
GET /api/v1/universitas/[id]
```

#### List semua universitas
```http
GET /api/v1/list/universitas
```

#### Tambah universitas baru
```http
POST /api/v1/add/universitas
```

#### Edit universitas
```http
POST /api/v1/edit/universitas/[id]
```

#### Nonaktifkan universitas
```http
DELETE /api/v1/universitas/[id]
```

#### Aktifkan kembali universitas
```http
PATCH /api/v1/universitas/[id]
```

### Struktur Data

```json
{
  "id": 123,
  "nama": "string",
  "english": "string|null",
  "kode": "string|null",
  "singkatan": "string|null",
  "website": "string|null",
  "aktif": true,
  "deskripsi": "string|null",
  "metadata": {
    "logo_kiri": "url|null",
    "logo_kanan": "url|null",
    "alamat_1": "string|null",
    "alamat_2": "string|null",
    "kontak_1": "string|null",
    "kontak_2": "string|null",
    "email_1": "string|null",
    "email_2": "string|null"
  }
}
```

### Catatan
- `id` adalah identitas unik universitas.
- `aktif` digunakan untuk menandai status aktif/nonaktif.
- `metadata` digunakan untuk menampung informasi tambahan seperti logo, alamat, kontak, dan email.

---

## Fakultas

Entitas **Fakultas** berada di bawah **Universitas**.  
Satu universitas dapat memiliki banyak fakultas.

### Endpoint

#### Ambil data fakultas berdasarkan ID
```http
GET /api/v1/fakultas/[id]
```

#### List semua fakultas pada universitas tertentu
```http
GET /api/v1/list/fakultas/[id_universitas]
```

#### Tambah fakultas baru
```http
POST /api/v1/add/fakultas
```

#### Edit fakultas
```http
POST /api/v1/edit/fakultas/[id]
```

#### Nonaktifkan fakultas
```http
DELETE /api/v1/fakultas/[id]
```

#### Aktifkan kembali fakultas
```http
PATCH /api/v1/fakultas/[id]
```

### Struktur Data

```json
{
  "id": 123,
  "id_universitas": 123,
  "nama": "string",
  "english": "string|null",
  "singkatan": "string|null",
  "website": "string|null",
  "aktif": true,
  "deskripsi": "string|null",
  "metadata": {
    "logo_kiri": "url|null",
    "logo_kanan": "url|null",
    "alamat_1": "string|null",
    "alamat_2": "string|null",
    "kontak_1": "string|null",
    "kontak_2": "string|null",
    "email_1": "string|null",
    "email_2": "string|null"
  }
}
```

### Catatan
- `id_universitas` menunjukkan bahwa fakultas terhubung ke universitas tertentu.
- Struktur `metadata` mengikuti pola yang serupa dengan entitas universitas.

---

## Prodi

Entitas **Prodi** berada di bawah **Fakultas**.  
Satu fakultas dapat memiliki banyak program studi.

### Endpoint

#### Ambil data prodi berdasarkan ID
```http
GET /api/v1/prodi/[id]
```

#### List semua prodi pada fakultas tertentu
```http
GET /api/v1/list/prodi/[id_fakultas]
```

#### Tambah prodi baru
```http
POST /api/v1/add/prodi
```

#### Edit prodi
```http
POST /api/v1/edit/prodi/[id]
```

#### Nonaktifkan prodi
```http
DELETE /api/v1/prodi/[id]
```

#### Aktifkan kembali prodi
```http
PATCH /api/v1/prodi/[id]
```

### Struktur Data

```json
{
  "id": 123,
  "id_fakultas": 123,
  "nama": "string",
  "english": "string|null",
  "kode": "string|null",
  "singkatan": "string|null",
  "jenjang": "string",
  "akreditasi": "string|null",
  "website": "string|null",
  "aktif": true,
  "deskripsi": "string|null",
  "metadata": {
    "alamat_1": "string|null",
    "alamat_2": "string|null",
    "kontak_1": "string|null",
    "kontak_2": "string|null",
    "email_1": "string|null",
    "email_2": "string|null"
  }
}
```

### Catatan
- `id_fakultas` menunjukkan relasi prodi ke fakultas.
- `jenjang` dapat digunakan untuk menyimpan nilai seperti `D3`, `S1`, `S2`, `S3`, atau bentuk lain sesuai kebutuhan.
- `akreditasi` bersifat opsional.

---

## TahunAjaran

Entitas **TahunAjaran** berada di bawah **Prodi** dan digunakan untuk mendefinisikan periode akademik.

### Endpoint

#### Ambil data tahun ajaran berdasarkan ID
```http
GET /api/v1/tahunajaran/[id]
```

#### List semua tahun ajaran pada prodi tertentu
```http
GET /api/v1/list/tahunajaran/[id_prodi]
```

#### Tambah tahun ajaran baru
```http
POST /api/v1/add/tahunajaran
```

#### Edit tahun ajaran
```http
POST /api/v1/edit/tahunajaran/[id]
```

#### Nonaktifkan tahun ajaran
```http
DELETE /api/v1/tahunajaran/[id]
```

#### Aktifkan kembali tahun ajaran
```http
PATCH /api/v1/tahunajaran/[id]
```

### Struktur Data

```json
{
  "id": 123,
  "id_prodi": 123,
  "nama": "string",
  "tahun": 2020,
  "periode": "GANJIL|GENAP|PENDEK",
  "aktif": true,
  "deskripsi": "string|null"
}
```

### Catatan
- `id_prodi` menunjukkan tahun ajaran milik prodi tertentu.
- `periode` menggunakan nilai terbatas:
  - `GANJIL`
  - `GENAP`
  - `PENDEK`

---

## Kurikulum

Entitas **Kurikulum** berada di bawah **Prodi** dan digunakan untuk mendefinisikan struktur kurikulum per tahun.

### Endpoint

#### Ambil data kurikulum berdasarkan ID
```http
GET /api/v1/kurikulum/[id]
```

#### List semua kurikulum pada prodi tertentu
```http
GET /api/v1/list/kurikulum/[id_prodi]
```

#### Tambah kurikulum baru
```http
POST /api/v1/add/kurikulum
```

#### Edit kurikulum
```http
POST /api/v1/edit/kurikulum/[id]
```

#### Nonaktifkan kurikulum
```http
DELETE /api/v1/kurikulum/[id]
```

#### Aktifkan kembali kurikulum
```http
PATCH /api/v1/kurikulum/[id]
```

### Struktur Data

```json
{
  "id": 123,
  "id_prodi": 123,
  "nama": "string",
  "tahun": 2020,
  "aktif": true,
  "deskripsi": "string|null"
}
```

### Catatan
- `id_prodi` menunjukkan kurikulum milik prodi tertentu.
- `tahun` dapat digunakan untuk menandai tahun mulai atau identitas kurikulum.

---

## ProfilLulusan

Entitas **ProfilLulusan** berada di bawah **Prodi** dan digunakan untuk mendefinisikan profil lulusan yang dituju.

### Endpoint

#### Ambil data profil lulusan berdasarkan ID
```http
GET /api/v1/profillulusan/[id]
```

#### List semua profil lulusan pada prodi tertentu
```http
GET /api/v1/list/profillulusan/[id_prodi]
```

#### Tambah profil lulusan baru
```http
POST /api/v1/add/profillulusan
```

#### Edit profil lulusan
```http
POST /api/v1/edit/profillulusan/[id]
```

#### Nonaktifkan profil lulusan
```http
DELETE /api/v1/profillulusan/[id]
```

#### Aktifkan kembali profil lulusan
```http
PATCH /api/v1/profillulusan/[id]
```

### Struktur Data

```json
{
  "id": 123,
  "id_prodi": 123,
  "nomor": 123,
  "nama": "string",
  "aktif": true,
  "deskripsi": "string|null"
}
```

### Catatan
- `nomor` dapat digunakan untuk pengurutan profil lulusan.
- `id_prodi` menunjukkan profil lulusan milik prodi tertentu.

---

## MasterCPL

Entitas **MasterCPL** berada di bawah **Kurikulum** dan berelasi dengan **ProfilLulusan**.  
Entitas ini merepresentasikan **Capaian Pembelajaran Lulusan (CPL)** pada level kurikulum.

### Endpoint

#### Ambil data master CPL berdasarkan ID
```http
GET /api/v1/mastercpl/[id]
```

#### List semua master CPL pada kurikulum tertentu
```http
GET /api/v1/list/mastercpl/[id_kurikulum]
```

#### Tambah master CPL baru
```http
POST /api/v1/add/mastercpl
```

#### Edit master CPL
```http
POST /api/v1/edit/mastercpl/[id]
```

#### Nonaktifkan master CPL
```http
DELETE /api/v1/mastercpl/[id]
```

#### Aktifkan kembali master CPL
```http
PATCH /api/v1/mastercpl/[id]
```

### Struktur Data

```json
{
  "id": 123,
  "id_kurikulum": 123,
  "id_profil_lulusan": 123,
  "nomor": 123,
  "nama": "string",
  "aktif": true,
  "deskripsi": "string|null"
}
```

### Catatan
- `id_kurikulum` menunjukkan CPL milik kurikulum tertentu.
- `id_profil_lulusan` menunjukkan keterkaitan CPL dengan profil lulusan.
- `nomor` dapat digunakan untuk penomoran CPL, misalnya `CPL-1`, `CPL-2`, dan seterusnya pada level aplikasi.

---

## MataKuliah

Entitas **MataKuliah** berada di bawah **Kurikulum**.  
Selain informasi dasar mata kuliah, entitas ini juga memuat konfigurasi:
- rentang nilai (`range`)
- bobot telusur dan evaluasi
- pemetaan CPL, CPMK, dan SCPMK
- relasi kontribusi evaluasi terhadap SCPMK

### Endpoint

#### Ambil data mata kuliah berdasarkan ID
```http
GET /api/v1/matakuliah/[id]
```

#### List semua mata kuliah pada kurikulum tertentu
```http
GET /api/v1/list/matakuliah/[id_kurikulum]
```

#### Tambah mata kuliah baru
```http
POST /api/v1/add/matakuliah
```

#### Edit mata kuliah
```http
POST /api/v1/edit/matakuliah/[id]
```

#### Nonaktifkan mata kuliah
```http
DELETE /api/v1/matakuliah/[id]
```

#### Aktifkan kembali mata kuliah
```http
PATCH /api/v1/matakuliah/[id]
```

### Struktur Data

```jsonc
{
  "id": 123,
  "id_kurikulum": 123,
  "kode": "string",
  "nama": "string",
  "english": "string|null",
  "semester": 123,
  "sks": 123,
  "pilihan": false,
  "wajib": true,
  "paket": false,
  "obe": true,
  "range": [
    { "id": 123, "nama": "A", "min": 85, "max": 100, "mode": ">=" },
    { "id": 123, "nama": "AB", "min": 75, "max": 85, "mode": ">" },
    { "id": 123, "nama": "B", "min": 70, "max": 75, "mode": ">" },
    { "id": 123, "nama": "BC", "min": 65, "max": 70, "mode": ">" },
    { "id": 123, "nama": "C", "min": 50, "max": 65, "mode": ">" },
    { "id": 123, "nama": "D", "min": 40, "max": 50, "mode": ">" },
    { "id": 123, "nama": "E", "min": 0, "max": 40, "mode": ">" }
    /* dan seterusnya */
  ],
  "bobot": {
    "telusur": [
      {
        "id": 123,
        "id_matakuliah": 123,
        "nama": "string",
        "bobot": 123.00,
        "aktif": true,
        "deskripsi": "string|null",
        "evaluasi": [
          {
            "id": 123,
            "id_telusur": 123,
            "nama": "string",
            "bobot": 123.00,
            "aktif": true,
            "deskripsi": "string|null"
          }
        ]
      }
    ],
    "cpl": [
      {
        /* CPL = Capaian Pembelajaran Lulusan */
        "id": 123,
        "id_matakuliah": 123,
        "id_master_cpl": 123,
        "nomor": 123,
        "nama": "string",
        "bobot": 123.00,
        "aktif": true,
        "deskripsi": "string|null",
        "cpmk": [
          {
            /* CPMK = Capaian Pembelajaran Mata Kuliah */
            "id": 123,
            "id_cpl": 123,
            "nomor": 123,
            "nama": "string",
            "bobot": 123.00,
            "aktif": true,
            "deskripsi": "string|null",
            "scpmk": [
              {
                /* SCPMK = Sub-Capaian Pembelajaran Mata Kuliah */
                "id": 123,
                "id_cpmk": 123,
                "nomor": 123,
                "nama": "string",
                "bobot": 123.00,
                "aktif": true,
                "deskripsi": "string|null"
              }
            ]
          }
        ]
      }
    ],
    "links": [
      /* Relasi many-to-many antara Evaluasi dan SCPMK */
      { "id": 123, "id_evaluasi": 123, "id_scpmk": 123, "bobot": 123.00, "aktif": true },
      { "id": 123, "id_evaluasi": 123, "id_scpmk": 123, "bobot": 123.00, "aktif": true }
    ]
  }
}
```

### Penjelasan Struktur Mata Kuliah

#### Informasi dasar
- `id_kurikulum`: relasi mata kuliah ke kurikulum.
- `kode`: kode mata kuliah.
- `nama`: nama mata kuliah.
- `english`: nama mata kuliah dalam bahasa Inggris.
- `semester`: semester penempatan mata kuliah.
- `sks`: jumlah SKS.
- `pilihan`: penanda apakah mata kuliah bersifat pilihan.
- `wajib`: penanda apakah mata kuliah bersifat wajib.
- `paket`: penanda apakah mata kuliah termasuk dalam paket.
- `obe`: penanda apakah mata kuliah mengikuti skema OBE.

#### Range nilai
Field `range` digunakan untuk menyimpan interval nilai huruf.  
Default dapat berupa skema `A` sampai `E`, namun dapat diperluas sesuai kebutuhan.

Contoh:
- `A`: 85–100
- `AB`: 75–85
- `B`: 70–75
- `BC`: 65–70
- `C`: 50–65
- `D`: 40–50
- `E`: 0–40

#### Bobot telusur dan evaluasi
Bagian `bobot.telusur` digunakan untuk mendefinisikan kelompok penelusuran penilaian pada mata kuliah.  
Setiap `telusur` dapat memiliki satu atau lebih `evaluasi`.

Contoh:
- Telusur: Tugas
- Evaluasi: Tugas 1, Tugas 2, Tugas Besar

#### Bobot CPL, CPMK, dan SCPMK
Bagian `bobot.cpl` digunakan untuk memetakan kontribusi mata kuliah terhadap CPL.  
Setiap CPL dapat diturunkan menjadi beberapa CPMK, lalu setiap CPMK dapat diturunkan lagi menjadi beberapa SCPMK.

Hierarki:
```text
CPL
└── CPMK
    └── SCPMK
```

#### Links evaluasi ke SCPMK
Bagian `bobot.links` digunakan untuk menyimpan relasi kontribusi antara `evaluasi` dengan `SCPMK`.

Karakteristik:
- bersifat **many-to-many**
- setiap relasi memiliki `bobot`
- relasi juga memiliki status `aktif`

---

## Catatan Umum

- Hampir semua entitas memiliki field `aktif` untuk mendukung mekanisme **soft delete**.
- Operasi `DELETE` pada dokumentasi ini diasumsikan sebagai **menonaktifkan**, bukan menghapus permanen dari basis data.
- Operasi `PATCH` digunakan untuk mengaktifkan kembali entitas yang sebelumnya dinonaktifkan.
- Struktur JSON di atas adalah struktur data konseptual awal dan dapat diperluas sesuai kebutuhan implementasi backend maupun frontend.

---

## Lanjutan

Dokumen ini saat ini baru mencakup:
- Universitas
- Fakultas
- Prodi
- TahunAjaran
- Kurikulum
- ProfilLulusan
- MasterCPL
- MataKuliah

Tahap berikutnya dapat dilanjutkan untuk entitas setelah **MataKuliah**.
