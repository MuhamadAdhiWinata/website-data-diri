# website-data-diri
Website data diri ini dibuat bertujuan untuk menyelesaikan Tugas Responsi Praktikum Teknologi Cloud

## Demo 

https://github.com/MuhamadAdhiWinata/website-data-diri/assets/142725576/dbaa4ff1-868d-441d-90dd-893a04025cbf

## Struktur Proyek
- ```website-profil/```
 ```index.html```
 ```foto.jpg```
 ```Dockerfile```

- ```website-utama/```
 ```index.html```
 ```Dockerfile```

## Persiapan
### Langkah 1: Membuat Direktori 
Pertama, buat dua direktori untuk website utama dan website profil, lalu masuk ke direktori profile.

```bash
mkdir website-utama website-profil
cd website-profil
```
### Langkah 2: Mengunduh Gambar
Unduh gambar menggunakan curl, disini saya mengupload/hosting foto saya ke imgbb.com .

```bash
curl https://i.ibb.co.com/1vYyrxq/foto.jpg -o foto.jpg
```
### Langkah 3: Membuat File HTML untuk Halaman Profil
Buat file index.html dengan konten berikut untuk halaman profil, disini saya menggunakan html dan css inline sederhana :

```bash
cat <<EOL > index.html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Halaman Profil</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #f4f4f4;
            text-align: center;
        }
        .container {
            max-width: 800px;
            margin: 50px auto;
            background: #fff;
            padding: 20px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }
        h1 {
            color: #333;
        }
        .profile-pic {
            width: 200px;
            height: 200px;
            border-radius: 50%;
            object-fit: cover;
            margin-bottom: 20px;
        }
        ul {
            list-style: none;
            padding: 0;
        }
        li {
            margin: 10px 0;
        }
        a {
            text-decoration: none;
            color: #007bff;
        }
        a:hover {
            text-decoration: underline;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Profil</h1>
        <a href="https://i.ibb.co.com/1vYyrxq/foto.jpg">
            <img src="foto.jpg" alt="Foto Profil" class="profile-pic" />
        </a>
        <h2>Link :</h2>
        <ul>
            <li>Github: <a href="https://github.com/MuhamadAdhiWinata">Muhamad Adhi Winata</a></li>
            <li>LinkedIn: <a href="https://www.linkedin.com/in/muhamad-adhi-winata-645427280/">Muhamad Adhi Winata</a></li>
        </ul>
    </div>
</body>
</html>
EOL
```

### Langkah 4: Membuat Dockerfile untuk website-profil
Buat file Dockerfile dengan bash berikut :

```bash
cat <<EOL > Dockerfile
FROM nginx:latest
COPY . /usr/share/nginx/html
EXPOSE 80
EOL
```
### Langkah 5: Membuat Jaringan Docker
Buat jaringan Docker untuk menghubungkan kedua kontainer, dengan bash berikut :

```bash
docker network create Muhamad-Adhi-Winata-network
```

### Langkah 6: Membangun dan Menjalankan Kontainer untuk website-profil
Bangun image Docker dan jalankan kontainer untuk website-profil.

```bash
docker build -t website-profil .
docker run -d --name website-profil --network Muhamad-Adhi-Winata-network -p 8081:80 website-profil
```
Uji dengan menjalankan halaman profil :

klik menu pada playground lalu pilih Traffic/Ports seperti yang tertera pada gambar : 

![Screenshot 2024-07-10 014013](https://github.com/MuhamadAdhiWinata/website-data-diri/assets/142725576/f0e6148e-8212-45d2-b7a4-51373e7be56f)

lalu custom ports menjadi 8081 seperti yang tertera di gambar lalu klik Acces : 

![Screenshot 2024-07-10 014227](https://github.com/MuhamadAdhiWinata/website-data-diri/assets/142725576/3d8400fa-64cc-4c56-83bd-7a4f1fd5d61d)

Jika langkah langkah yang dilakukan sudah benar maka akan tampil Halaman Profil Berikut :

![Screenshot 2024-07-10 014911](https://github.com/MuhamadAdhiWinata/website-data-diri/assets/142725576/a54630f7-d9be-499f-a87c-373294e419e7)

lalu copy domain yang ada pada halaman profil contoh :

![Screenshot 2024-07-10 015703](https://github.com/MuhamadAdhiWinata/website-data-diri/assets/142725576/e60e92df-0dad-4126-97e2-5d683ce2dc56)

### Langkah 7: Membuat File HTML untuk Halaman Utama
Masuk ke direktori website-utama dan buat file index.html yang menampilkan Nama Lengkap, NIM, Program Studi, Hobi, dan Link ke halaman profil untuk halaman utama. Dengan bash berikut lalu **paste/letakkan link domain dari halaman profil ke ```<a href="...">Profil</a>``` yang memiliki keterangan titik titik  “ ... ” :**

```bash
cd ../website-utama
cat <<EOL > index.html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Halaman Utama</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #f4f4f4;
            text-align: center;
        }
        .container {
            max-width: 800px;
            margin: 50px auto;
            background: #fff;
            padding: 20px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }
        h1 {
            color: #333;
        }
        p {
            font-size: 18px;
            color: #555;
        }
        a {
            text-decoration: none;
            color: #007bff;
            font-weight: bold;
        }
        a:hover {
            text-decoration: underline;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Data Diri</h1>
        <p>Nama Lengkap: Muhamad Adhi Winata</p>
        <p>NIM: 215610059</p>
        <p>Program Studi: Sistem Informasi</p>
        <p>Hobi: Memasak </p>
        <a href="...">Profil</a>
    </div>
</body>
</html>
EOL
```

### Langkah 8: Membuat Dockerfile untuk website-utama
Buat file Dockerfile dengan bash berikut:

```bash
cat <<EOL > Dockerfile
FROM nginx:latest
COPY . /usr/share/nginx/html
EXPOSE 80
EOL
```

### Langkah 9: Membangun dan Menjalankan Kontainer untuk website-utama
Bangun image Docker dan jalankan kontainer untuk website-utama.

```bash
docker build -t website-utama .
docker run -d --name website-utama --network Muhamad-Adhi-Winata-network -p 8080:80 website-utama
```

# Pengujian

Lalu Jalankan dengan : 
klik menu pada playground lalu pilih Traffic/Ports seperti yang tertera pada gambar : 

![Screenshot 2024-07-10 014013](https://github.com/MuhamadAdhiWinata/website-data-diri/assets/142725576/573f20c5-d8d4-4346-8053-c16cadf1ab8c)

lalu custom ports menjadi 8080 seperti yang tertera di gambar lalu klik Acces :

![Screenshot 2024-07-10 021119](https://github.com/MuhamadAdhiWinata/website-data-diri/assets/142725576/4999870e-a0c7-440e-a1d4-3504b8b02113)

Jika langkah langkah yang dilakukan sudah benar maka akan tampil Halaman Utama Berikut :

![Screenshot 2024-07-10 021344](https://github.com/MuhamadAdhiWinata/website-data-diri/assets/142725576/f3cdfc06-d1bb-4d0c-a135-ed389475542f)

klik link profil maka akan menuju ke halaman profil :

![Screenshot 2024-07-10 014911](https://github.com/MuhamadAdhiWinata/website-data-diri/assets/142725576/4500b41c-09ec-47c9-99dc-61245e4e9048)


## 🚀 Authors

- [@MuhamadAdhiWinata](https://www.github.com/MuhamadAdhiWinata)
