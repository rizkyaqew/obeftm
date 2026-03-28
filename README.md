# OBE FTM Unjani

Dokumentasi awal struktur data dan endpoint untuk aplikasi **OBE FTM Unjani**.  
Dokumen ini saat ini mencakup entitas master sampai dengan **MataKuliah**.

---

## Daftar Isi

- [Struktur Data](#struktur-data)
  - [Universitas](#universitas)
  - [Fakultas](#fakultas)
  - [Prodi](#prodi)
  - [TahunAjaran](#tahunajaran)
  - [Kurikulum](#kurikulum)
  - [ProfilLulusan](#profillulusan)
  - [MasterCPL](#mastercpl)
  - [MataKuliah](#matakuliah)
- [Konvensi Endpoint](#konvensi-endpoint)
- [Endpoint per Entitas](#endpoint-per-entitas)
  - [Universitas Endpoint](#universitas-endpoint)
  - [Fakultas Endpoint](#fakultas-endpoint)
  - [Prodi Endpoint](#prodi-endpoint)
  - [TahunAjaran Endpoint](#tahunajaran-endpoint)
  - [Kurikulum Endpoint](#kurikulum-endpoint)
  - [ProfilLulusan Endpoint](#profillulusan-endpoint)
  - [MasterCPL Endpoint](#mastercpl-endpoint)
  - [MataKuliah Endpoint](#matakuliah-endpoint)

---

# Struktur Data

## Universitas

Entitas **Universitas** adalah level tertinggi dalam struktur data.  
Satu universitas dapat menaungi banyak fakultas.

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

### Keterangan
- `id`: identitas unik universitas.
- `nama`: nama universitas.
- `english`: nama universitas dalam bahasa Inggris.
- `kode`: kode universitas.
- `singkatan`: singkatan universitas.
- `website`: alamat situs resmi universitas.
- `aktif`: status aktif/nonaktif.
- `deskripsi`: keterangan tambahan.
- `metadata`: informasi tambahan seperti logo, alamat, kontak, dan email.

---

## Fakultas

Entitas **Fakultas** berada di bawah **Universitas**.  
Satu universitas dapat memiliki banyak fakultas.

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

### Keterangan
- `id_universitas`: relasi ke universitas induk.
- Struktur `metadata` mengikuti pola yang mirip dengan entitas universitas.

---

## Prodi

Entitas **Prodi** berada di bawah **Fakultas**.  
Satu fakultas dapat memiliki banyak program studi.

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

### Keterangan
- `id_fakultas`: relasi ke fakultas induk.
- `jenjang`: contoh `D3`, `S1`, `S2`, `S3`, dan seterusnya.
- `akreditasi`: status atau peringkat akreditasi program studi.

---

## TahunAjaran

Entitas **TahunAjaran** berada di bawah **Prodi** dan digunakan untuk mendefinisikan periode akademik.

```json
{
  "id": 123,
  "id_prodi": 123,
  "nama": "string",
  "tahun_awal": 2020,
  "tahun_akhir": 2021,
  "periode": "GANJIL|GENAP|PENDEK",
  "aktif": true,
  "deskripsi": "string|null"
}
```

### Keterangan
- `id_prodi`: relasi ke prodi induk.
- `tahun`: tahun akademik.
- `periode`: salah satu dari:
  - `GANJIL`
  - `GENAP`
  - `PENDEK`

---

## Kurikulum

Entitas **Kurikulum** berada di bawah **Prodi** dan digunakan untuk mendefinisikan struktur kurikulum.

```json
{
  "id": 123,
  "id_prodi": 123,
  "kode": "string",
  "nama": "string",
  "tahun": 2020,
  "aktif": true,
  "deskripsi": "string|null"
}
```

### Keterangan
- `id_prodi`: relasi ke prodi induk.
- `tahun`: tahun kurikulum.
- `aktif`: status aktif/nonaktif kurikulum.

---

## ProfilLulusan

Entitas **ProfilLulusan** berada di bawah **Prodi** dan digunakan untuk mendefinisikan profil lulusan yang dituju.

```json
{
  "id": 123,
  "id_prodi": 123,
  "nomor": 123,
  "jenis": "UTAMA|TAMABAHAN",
  "nama": "string",
  "aktif": true,
  "deskripsi": "string|null"
}
```

### Keterangan
- `id_prodi`: relasi ke prodi induk.
- `nomor`: nomor urut profil lulusan.
- `nama`: nama profil lulusan.

---

## MasterCPL

Entitas **MasterCPL** berada di bawah **Kurikulum** dan berelasi dengan **ProfilLulusan**.  
Entitas ini merepresentasikan **Capaian Pembelajaran Lulusan (CPL)**.

```json
{
  "id": 123,
  "id_kurikulum": 123,
  "id_profil_lulusan": 123,
  "nomor": 123,
  "nama": "string",
  "aktif": true,
  "deskripsi_id": "string|null",
  "deskripsi_en": "string|null"
}
```

### Keterangan
- `id_kurikulum`: relasi ke kurikulum induk.
- `id_profil_lulusan`: relasi ke profil lulusan.
- `nomor`: nomor urut CPL.
- `nama`: nama CPL.

---

## MataKuliah

Entitas **MataKuliah** berada di bawah **Kurikulum**.  
Selain data dasar mata kuliah, entitas ini juga memuat:
- rentang nilai,
- bobot telusur dan evaluasi,
- relasi CPL, CPMK, SCPMK,
- serta kontribusi evaluasi terhadap SCPMK.

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
            "id": 123,
            "id_cpl": 123,
            "nomor": 123,
            "nama": "string",
            "bobot": 123.00,
            "aktif": true,
            "deskripsi": "string|null",
            "scpmk": [
              {
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
      { "id": 123, "id_evaluasi": 123, "id_scpmk": 123, "bobot": 123.00, "aktif": true },
      { "id": 123, "id_evaluasi": 123, "id_scpmk": 123, "bobot": 123.00, "aktif": true }
    ]
  }
}
```

### Keterangan

#### Informasi dasar
- `id_kurikulum`: relasi ke kurikulum induk.
- `kode`: kode mata kuliah.
- `nama`: nama mata kuliah.
- `english`: nama mata kuliah dalam bahasa Inggris.
- `semester`: semester penempatan mata kuliah.
- `sks`: jumlah SKS.
- `pilihan`: penanda apakah mata kuliah pilihan.
- `wajib`: penanda apakah mata kuliah wajib.
- `paket`: penanda apakah mata kuliah merupakan bagian dari paket.
- `obe`: penanda apakah mata kuliah mengikuti skema OBE.

#### Range nilai
Field `range` digunakan untuk menyimpan rentang nilai huruf.  
Default dapat berupa `A` sampai `E`, dan dapat dikembangkan sesuai kebutuhan.

#### Bobot telusur
`bobot.telusur` menyimpan kelompok penelusuran penilaian.  
Setiap telusur dapat memiliki satu atau lebih `evaluasi`.

#### Bobot CPL, CPMK, SCPMK
Hierarki pembelajaran pada mata kuliah mengikuti struktur berikut:

```text
CPL
└── CPMK
    └── SCPMK
```

#### Links
`bobot.links` menyimpan relasi kontribusi **many-to-many** antara `evaluasi` dan `SCPMK`.

---

# Konvensi Endpoint

Struktur endpoint umum yang digunakan adalah sebagai berikut.

## 1. Akses sebuah entitas

```http
GET /api/v1/[nama_entitas]/[id]
```

## 2. List semua entitas

```http
GET /api/v1/list/[nama_entitas]/[id_parent]
```

> **Catatan:** khusus entitas **Universitas**, `[id_parent]` tidak diperlukan.

## 3. Insert entitas baru

```http
POST /api/v1/add/[nama_entitas]
```

## 4. Update sebuah entitas

```http
POST /api/v1/edit/[nama_entitas]/[id]
```

## 5. Nonaktifkan sebuah entitas

```http
DELETE /api/v1/[nama_entitas]/[id]
```

## 6. Aktifkan kembali sebuah entitas

```http
PATCH /api/v1/[nama_entitas]/[id]
```

---

# Endpoint per Entitas

## Universitas Endpoint

```http
GET /api/v1/universitas/[id]
GET /api/v1/list/universitas
POST /api/v1/add/universitas
POST /api/v1/edit/universitas/[id]
DELETE /api/v1/universitas/[id]
PATCH /api/v1/universitas/[id]
```

---

## Fakultas Endpoint

```http
GET /api/v1/fakultas/[id]
GET /api/v1/list/fakultas/[id_universitas]
POST /api/v1/add/fakultas
POST /api/v1/edit/fakultas/[id]
DELETE /api/v1/fakultas/[id]
PATCH /api/v1/fakultas/[id]
```

---

## Prodi Endpoint

```http
GET /api/v1/prodi/[id]
GET /api/v1/list/prodi/[id_fakultas]
POST /api/v1/add/prodi
POST /api/v1/edit/prodi/[id]
DELETE /api/v1/prodi/[id]
PATCH /api/v1/prodi/[id]
```

---

## TahunAjaran Endpoint

```http
GET /api/v1/tahunajaran/[id]
GET /api/v1/list/tahunajaran/[id_prodi]
POST /api/v1/add/tahunajaran
POST /api/v1/edit/tahunajaran/[id]
DELETE /api/v1/tahunajaran/[id]
PATCH /api/v1/tahunajaran/[id]
```

---

## Kurikulum Endpoint

```http
GET /api/v1/kurikulum/[id]
GET /api/v1/list/kurikulum/[id_prodi]
POST /api/v1/add/kurikulum
POST /api/v1/edit/kurikulum/[id]
DELETE /api/v1/kurikulum/[id]
PATCH /api/v1/kurikulum/[id]
```

---

## ProfilLulusan Endpoint

```http
GET /api/v1/profillulusan/[id]
GET /api/v1/list/profillulusan/[id_prodi]
POST /api/v1/add/profillulusan
POST /api/v1/edit/profillulusan/[id]
DELETE /api/v1/profillulusan/[id]
PATCH /api/v1/profillulusan/[id]
```

---

## MasterCPL Endpoint

```http
GET /api/v1/mastercpl/[id]
GET /api/v1/list/mastercpl/[id_kurikulum]
POST /api/v1/add/mastercpl
POST /api/v1/edit/mastercpl/[id]
DELETE /api/v1/mastercpl/[id]
PATCH /api/v1/mastercpl/[id]
```

---

## MataKuliah Endpoint

```http
GET /api/v1/matakuliah/[id]
GET /api/v1/list/matakuliah/[id_kurikulum]
POST /api/v1/add/matakuliah
POST /api/v1/edit/matakuliah/[id]
DELETE /api/v1/matakuliah/[id]
PATCH /api/v1/matakuliah/[id]
```

---

## Catatan Umum

- Hampir semua entitas memiliki field `aktif` untuk mendukung **soft delete**.
- Operasi `DELETE` pada dokumentasi ini dimaksudkan sebagai **menonaktifkan**, bukan menghapus permanen dari basis data.
- Operasi `PATCH` digunakan untuk mengaktifkan kembali data yang sebelumnya dinonaktifkan.
- Struktur JSON pada dokumen ini adalah struktur konseptual awal dan masih dapat dikembangkan sesuai implementasi backend maupun frontend.

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
