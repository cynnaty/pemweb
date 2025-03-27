**Analisis 5W + 1H - Mata Kuliah Pemrograman Web**

## 1. **Pendahuluan**

Pembuatan web dalam mata kuliah Pemrograman Web dilakukan dengan menggunakan berbagai alat dan teknologi, termasuk Docker, VS Code, terminal WSL Ubuntu, dan Chrome. Proses ini melibatkan penggunaan Nginx sebagai web server serta pengelolaan proyek menggunakan Docker Compose.

## - **Mengapa Menggunakan Docker?**

Docker digunakan dalam proyek ini karena menyediakan lingkungan pengembangan yang terisolasi, mempermudah pengelolaan dependensi, dan memastikan bahwa aplikasi berjalan secara konsisten di berbagai sistem operasi. Dengan Docker, semua konfigurasi dan file proyek dapat dikemas dalam sebuah container sehingga mudah untuk dideploy tanpa perlu konfigurasi tambahan di setiap mesin baru.

## - **Kelebihan dan Kekurangan Docker**

### **Kelebihan:**
- **Portabilitas**: Dapat dijalankan di berbagai sistem tanpa harus mengonfigurasi ulang.
- **Konsistensi**: Lingkungan pengembangan dan produksi tetap seragam.
- **Isolasi**: Menghindari konflik dependensi antar proyek.
- **Efisiensi**: Lebih ringan dibandingkan virtual machine karena berbasis container.

### **Kekurangan:**
- **Kinerja**: Meskipun ringan, Docker masih memiliki overhead dibandingkan aplikasi yang berjalan langsung di sistem host.
- **Keamanan**: Jika tidak dikonfigurasi dengan baik, dapat menimbulkan celah keamanan.
- **Kurva Pembelajaran**: Memerlukan pemahaman yang cukup dalam tentang sistem containerization.

## 2. **Analisis 5W+1H**

**1. What (Apa yang dilakukan?)**  
Mahasiswa melakukan aktivitas pembuatan website dalam mata kuliah Pemrograman Web. Proses ini mencakup instalasi dan konfigurasi lingkungan kerja menggunakan Docker, VS Code, WSL Ubuntu, dan Chrome, serta pembuatan struktur folder dan file yang diperlukan untuk pengembangan web.

**2. Who (Siapa yang melakukannya?)**  
Mahasiswa yang mengikuti mata kuliah Pemrograman Web.

**3. When (Kapan dilakukan?)**  
Aktivitas dilakukan pada hari perkuliahan sesuai jadwal mata kuliah Pemrograman Web.

**4. Where (Di mana dilakukan?)**  
Dilakukan pada lingkungan perkuliahan, baik secara daring maupun luring, menggunakan komputer atau laptop dengan sistem operasi yang mendukung WSL Ubuntu dan Docker.

**5. Why (Mengapa dilakukan?)**  
Tujuan dari aktivitas ini adalah untuk memahami cara kerja pengembangan web menggunakan teknologi kontainerisasi seperti Docker, serta mempelajari struktur dan konfigurasi dasar dalam pembuatan website.

**6. How (Bagaimana cara melakukannya?)**  
Proses dilakukan dengan langkah-langkah berikut:

### a. **Persiapan Lingkungan Pengembangan**

1. Membuka terminal untuk navigasi dan pembuatan folder proyek.
2. Membuat direktori kerja baru dengan perintah:
   ```sh
   cd perkuliahan
   mkdir pemweb
   code .
   ```
   - `cd perkuliahan`: Masuk ke direktori perkuliahan.
   - `mkdir pemweb`: Membuat folder baru bernama "pemweb".
   - `code .`: Membuka VS Code dalam folder tersebut.
3. Menginstal ekstensi pada VS Code:
   - Auto Close Tag
   - Auto Complete Tag
   - Auto Rename Tag

### b. **Struktur Direktori**

Struktur proyek dibangun dengan berbagai folder dan file untuk mendukung pengembangan:

- `pemweb/`
  - `pertemuan1/`
    - `coding/`
      - `latihan/`
        - `home.html`
        - `profile.html`
      - `nginx/`
        - `nginx.conf`
      - `src/`
        - `html/`
          - `index.html`
        - `assets/`
      - `.env`
      - `docker-compose.yml`
    - `catatan.md`
    - `analisa.md`

### c. **Konfigurasi Nginx**

File `nginx.conf` berisi konfigurasi server yang menentukan bagaimana Nginx melayani file statis dari folder yang telah dibuat:

```nginx
server {
    listen 80;
    server_name localhost;

    root /usr/share/nginx/html;
    index index.html index.htm;

    location / {
        try_files $uri $uri/ =404;
    }

    location /latihan {
        alias /usr/share/nginx/latihan/;
        index index.html index.htm home.html;
        try_files $uri $uri.html $uri/ =404;
    }
}
```

**Penjelasan:**

- Mendefinisikan server yang berjalan di port `80`.
- Root direktori untuk web ditentukan sebagai `/usr/share/nginx/html`.
- Direktori `latihan` ditetapkan dengan alias `/usr/share/nginx/latihan/`.

### d. **Konfigurasi Environment File (.env)**

File `.env` digunakan untuk menyimpan variabel lingkungan:

```env
COMPOSE_PROJECT_NAME=esgul
REPOSITORY_NAME=pemweb
IMAGE_TAG=latest
```

**Penjelasan:**

- `COMPOSE_PROJECT_NAME`: Nama proyek Docker Compose.
- `REPOSITORY_NAME`: Nama repositori proyek.
- `IMAGE_TAG`: Tag versi image Docker.

### e. **Konfigurasi Docker Compose**

File `docker-compose.yml` digunakan untuk menjalankan layanan berbasis Docker:

```yaml
version: '3'

services:
  web:
    image: nginx:latest
    ports:
      - 80:80
    volumes:
      - ./nginx/nginx.conf:/etc/nginx/conf.d/default.conf
      - ./src:/usr/share/nginx/html
      - ./latihan:/usr/share/nginx/latihan
```

**Penjelasan:**

- Menggunakan image `nginx:latest` untuk container web.
- Memetakan port `80` dari container ke host.
- Memasang konfigurasi nginx (`nginx.conf`) dan folder sumber web (`src`, `latihan`) ke dalam container.

### f. **Menjalankan Proyek dengan Docker**

1. Membuka aplikasi Docker.
2. Menjalankan perintah berikut untuk membangun dan menjalankan container:
   ```sh
   docker compose up -d --build
   ```
   - `-d`: Menjalankan container di background.
   - `--build`: Membangun ulang image sebelum menjalankan.

### g. **Menguji Aplikasi Web**

1. Mengisi file `index.html`, `home.html`, dan `profile.html` sesuai kebutuhan.
2. Membuka browser dan mengetikkan `localhost` untuk mengakses aplikasi.

## 3. **Kesimpulan**

Proses pembuatan web ini mencakup berbagai aspek, mulai dari persiapan lingkungan pengembangan, pembuatan struktur direktori, konfigurasi Nginx, hingga implementasi Docker untuk pengelolaan container. Dengan pendekatan ini, proyek web dapat dijalankan dalam lingkungan yang lebih terstruktur dan mudah dikelola.