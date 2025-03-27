pada mata kuliah pemrograman web pertemuan 1, aktivitas yang lakukan yaitu membuat web

untuk aplikasinya memakai docker, vs code system, terminal WSL ubuntu, dan chrome

- pertama-tama buka terminal

- lalu ketik cd perkuliahan

- lalu ketik mkdir pemweb

- lalu ketik code .

- dan terbukalah vs code

- lalu download extension auto close tag, auto complete tag, dan auto rename tag

- lalu di folder pemweb buat folder pertemuan 1

- lalu di folder pertemuan1 buat folder coding, file catatan.md, dan file analisa.md

- lalu di folder coding buat folder latihan, folder nginx, folder src, file .env, dan file docker-compose.yml

- lalu di folder nginx buat file nginx.conf

- lalu di folder src buat folder html, dan folder assets

- lalu di folder html buat file index.html

- lalu di folder latihan buat file home.html, dan file profile.html

lalu isi file nginx.conf dengan:

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

lalu isi file .env dengan:

    COMPOSE_PROJECT_NAME=esgul
    REPOSITORY_NAME=pemweb
    IMAGE_TAG=latest

lalu isi file docker-compose.yml dengan:

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

- setelah mengisi file docker-compose.yml, file .env, dan file nginx.conf 

- selanjutnya buka aplikasi docker

- selanjutnya di terminal tadi, ketik docker compose up -d --build untuk meruning docker

- lalu isi file home.html, profile.html, index.html di folder html, dan index.html di folder src sesuai dengan yang kita inginkan

- setelah mengisi file home.html, profile.html, index.html di folder html, dan index.html di folder src

- lalu setelah itu ketik localhost di chrome

- dan kita sudah bisa melihat web ini di chrome

untuk file catatan.md berisi file ini sendiri 