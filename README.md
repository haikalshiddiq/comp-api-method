1. Install Python Install Manager terlebih dahulu di Microsoft Store
2. Extract file .zipnya
3. Lalu jalankan command 
4. cd direktori_hasil_extract
5. py server.py


##Instruksi Lengkap##

# REST API Methods Demo: POST, PUT, PATCH, DELETE

Demo ini dibuat untuk praktikum Communication Protocols ketika public fake API seperti JSONPlaceholder atau My JSON Server tidak merefleksikan perubahan data setelah `POST`, `PUT`, `PATCH`, atau `DELETE`.

## Kenapa Tidak Pakai JSONPlaceholder Saja?

JSONPlaceholder dan My JSON Server menerima method selain `GET`, tetapi mutation-nya bersifat simulasi. Response seolah-olah sukses, tetapi perubahan tidak disimpan permanen. Untuk mengajar konsep CRUD yang benar-benar terlihat berubah, gunakan API lokal ini.

## Fitur Endpoint

Base URL:

```text
http://localhost:8000
```

| Method | Endpoint | Fungsi |
|---|---|---|
| GET | `/api/products` | Ambil semua product |
| GET | `/api/products/{id}` | Ambil product berdasarkan id |
| POST | `/api/products` | Buat product baru |
| PUT | `/api/products/{id}` | Replace seluruh product |
| PATCH | `/api/products/{id}` | Update sebagian field |
| DELETE | `/api/products/{id}` | Hapus product |
| POST | `/api/reset` | Reset data ke seed awal |

## Cara Menjalankan

Windows:

```powershell
cd rest-api-methods-demo
py server.py
```

macOS/Linux:

```bash
cd rest-api-methods-demo
python3 server.py
```

Buka browser:

```text
http://localhost:8000
```

## Curl Demo

GET semua product:

```bash
curl -i http://localhost:8000/api/products
```

POST product baru:

Windows PowerShell:

```powershell
curl.exe -i -X POST http://localhost:8000/api/products -H 'Content-Type: application/json' -d '{"name":"Smart Sensor","category":"iot","price":175000,"stock":12}'
```

macOS/Linux:

```bash
curl -i -X POST http://localhost:8000/api/products \
  -H "Content-Type: application/json" \
  -d '{"name":"Smart Sensor","category":"iot","price":175000,"stock":12}'
```

PUT replace product id 1:

Windows PowerShell:

```powershell
curl.exe -i -X PUT http://localhost:8000/api/products/1 -H 'Content-Type: application/json' -d '{"name":"Laptop Pro 14 Replacement","category":"computer","price":15500000,"stock":4}'
```

macOS/Linux:

```bash
curl -i -X PUT http://localhost:8000/api/products/1 \
  -H "Content-Type: application/json" \
  -d '{"name":"Laptop Pro 14 Replacement","category":"computer","price":15500000,"stock":4}'
```

PATCH sebagian field product id 1:

Windows PowerShell:

```powershell
curl.exe -i -X PATCH http://localhost:8000/api/products/1 -H 'Content-Type: application/json' -d '{"stock":2,"price":14900000}'
```

macOS/Linux:

```bash
curl -i -X PATCH http://localhost:8000/api/products/1 \
  -H "Content-Type: application/json" \
  -d '{"stock":2,"price":14900000}'
```

DELETE product id 1:

```bash
curl -i -X DELETE http://localhost:8000/api/products/1
```

Cek hasil setelah delete:

```bash
curl -i http://localhost:8000/api/products/1
curl -i http://localhost:8000/api/products
```

Reset data:

```bash
curl -i -X POST http://localhost:8000/api/reset
```

## Alur Praktikum Dosen

1. Tunjukkan JSONPlaceholder: `POST` sukses tetapi `GET` berikutnya tidak berubah.
2. Jalankan API lokal ini.
3. Tunjukkan `GET /api/products`.
4. Lakukan `POST`, lalu `GET` lagi dan tunjukkan product baru muncul.
5. Lakukan `PUT`, lalu `GET /api/products/{id}` dan tunjukkan seluruh object berubah.
6. Lakukan `PATCH`, lalu tunjukkan hanya field tertentu berubah.
7. Lakukan `DELETE`, lalu tunjukkan `GET /api/products/{id}` menjadi `404`.
8. Import Postman collection dari folder `postman/`.

Untuk alur yang sepenuhnya memakai Postman, gunakan:

```text
postman-praktikum-guide.md
```

## Common Mistakes

- Body JSON tidak valid.
- Header `Content-Type: application/json` lupa ditambahkan.
- Menggunakan PowerShell alias `curl` tanpa `curl.exe`.
- Mengira `PUT` sama dengan `PATCH`.
- Setelah `DELETE`, masih mengecek response DELETE saja, bukan melakukan `GET` ulang untuk membuktikan resource hilang.

