# MINGGU 12
# DInstall Drupal with Docker Compose  
* https://www.linode.com/docs/quick-answers/linux/drupal-with-docker-compose/

1. Jalankan Docker terlebih dahulu kemudian masuk ke folder projeck anda   
2. Membuat folder dengan nama my-drupal  
<pre>
Student@DESKTOP-B8ACH4F MINGW64 ~/Documents/tcc/minggu-12 (master)
$ mkdir my_drupal
</pre>
3. Masuk ke root folder yang di buat  
<pre>  
Student@DESKTOP-B8ACH4F MINGW64 ~/Documents/tcc/minggu-12 (master)
$ cd
my_drupal/ README.md

Student@DESKTOP-B8ACH4F MINGW64 ~/Documents/tcc/minggu-12 (master)
$ cd my_drupal
</pre>  
4. Buat File dengan nama docker-compose.yml dan isikan script berikut  
<pre>
version: '3.3'

services:
  drupal:
    image: drupal:latest
    ports:
      - 9090:80
    volumes:
      - drupal_modules:/var/www/html/modules
      - drupal_profiles:/var/www/html/profiles
      - drupal_themes:/var/www/html/themes
      - drupal_sites:/var/www/html/sites
    restart: always

  postgres:
    image: postgres:10
    environment:
      POSTGRES_PASSWORD: your_postgres_password
    volumes:
        - db_data:/var/lib/postgresql/data
    restart: always

volumes:
  drupal_modules:
  drupal_profiles:
  drupal_themes:
  drupal_sites:
  db_data:
</pre>   
5. Jalankan Docker compose dengan perintah , sebelum menjalankan perintah Run Pasangkan ini pada command line (export COMPOSE_TLS_VERSION=TLSv1_2)  
<pre>
Student@DESKTOP-B8ACH4F MINGW64 ~/Documents/tcc/minggu-12/my_drupal (master)
$ export COMPOSE_TLS_VERSION=TLSv1_2

Student@DESKTOP-B8ACH4F MINGW64 ~/Documents/tcc/minggu-12/my_drupal (master)
$ docker-compose up -d
Creating network "mydrupal_default" with the default driver
Creating volume "mydrupal_db_data" with default driver
Creating volume "mydrupal_drupal_sites" with default driver
Creating volume "mydrupal_drupal_profiles" with default driver
Creating volume "mydrupal_drupal_themes" with default driver
Creating volume "mydrupal_drupal_modules" with default driver
Pulling drupal (drupal:latest)...
latest: Pulling from library/drupal
d599a449871e: Pull complete
1a363f133ddd: Pull complete
dd6ffd5f60d7: Pull complete
515e48bcd87c: Pull complete
c6f3d43db193: Pull complete
f1c6f8e807f6: Pull complete
65d8fe3b5a08: Pull complete
80429671c76c: Pull complete
053b8d72a5a3: Pull complete
deb7baf580dc: Pull complete
f2cdd5ef44df: Pull complete
bcace1d72fd7: Pull complete
b1995a0f5927: Pull complete
64c62b87d7fe: Pull complete
e52a9e2cc747: Pull complete
36f8406950cf: Pull complete
Digest: sha256:5c66427ae8826b1157ce0cf64db93feee694a0a5e4192dea341089285f8ace4a
Status: Downloaded newer image for drupal:latest
Pulling postgres (postgres:10)...
10: Pulling from library/postgres
d599a449871e: Already exists
eadd55e4a4ae: Pull complete
17eea069a47f: Pull complete
22b703021b03: Pull complete
5fa72174baec: Pull complete
338e0b17322b: Pull complete
05fd528a5e36: Pull complete
c224328d751f: Pull complete
f4319784a7ce: Pull complete
6b0ef024e116: Pull complete
5bc4176bd4c3: Pull complete
79c29b3c031a: Pull complete
9419079907eb: Pull complete
4b9b9c707beb: Pull complete
Digest: sha256:74e63f8b55e9b0ca55b78abb203d01e47c5ac7d3f10af09f91d5932943c6bb14
Status: Downloaded newer image for postgres:10
Creating mydrupal_postgres_1 ...
Creating mydrupal_drupal_1 ...
Creating mydrupal_postgres_1
Creating mydrupal_postgres_1 ... done
</pre>  
* -d artinya di jalankan di belakang background  




















