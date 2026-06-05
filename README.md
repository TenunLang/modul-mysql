# modul-mysql

Klien MySQL/MariaDB untuk bahasa [Tenun](https://github.com/TenunLang/Tenun), ditulis sepenuhnya dengan Tenun. Mendukung autentikasi `mysql_native_password` dan eksekusi query.

## Pasang

```
tenun add mysql
```

(mengkloning repo ini ke `./tenun_modul/mysql`)

## Pakai

```tenun
impor "mysql";

biar db: bulat = mysqlSambung("127.0.0.1", 3306, "root", "");
kalau db < 0 {
    cetak("gagal login");
} lain {
    biar hasil: teks = mysqlPerintah(db, "SELECT VERSION()");
    cetak(hasil);
    tutup(db);
}
```

## Fungsi

- `mysqlSambung(inang: teks, port: bulat, pengguna: teks, sandi: teks): bulat`
  Menyambung + autentikasi. Mengembalikan handle soket, atau `-1` bila gagal.
- `mysqlPerintah(soket: bulat, sql: teks): teks`
  Menjalankan perintah SQL (COM_QUERY). Mengembalikan respons mentah server.

Tutup koneksi dengan builtin inti `tutup(soket)`.

## Struktur

```
modul-mysql/
  tenun.json         manifest (nama, versi, deskripsi, berkas, butuh)
  src/
    mysql.tenun      sumber modul
  contoh/
    contoh.tenun     contoh pemakaian
  .github/workflows/ci.yml
  README.md
```

Entry modul ditunjuk oleh `berkas` di `tenun.json` (`src/mysql.tenun`).

## Catatan

- Saat ini `mysqlPerintah` mengembalikan paket respons mentah; parser hasil (baris/kolom) menyusul.
- Mendukung sandi kosong maupun `mysql_native_password`.

## Lisensi

MIT.
