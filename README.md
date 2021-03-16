<h1 align="center"><img src="https://raw.githubusercontent.com/LycheeOrg/Lychee/master/Banner.png"></h1>

[Sekilas Tentang](#sekilas-tentang) | [Instalasi](#instalasi) | [Konfigurasi](#konfigurasi) | [Otomatisasi](#otomatisasi) | [Cara Pemakaian](#cara-pemakaian) | [Pembahasan](#pembahasan) | [Referensi](#referensi)
:---:|:---:|:---:|:---:|:---:|:---:|:---:



# Sekilas Tentang
[`^ kembali ke atas ^`](#)

**Lychee** merupakan *photo-management-system* yang dapat diakses secara gratis. Semenjak 1 April 2018 , **Lychee** berada pada naungan organisasinya sendiri (*LycheeOrg*) dimana semua orang dapat menambahkan perbaikan pada **Lychee**.

# Instalasi
[`^ kembali ke atas ^`](#)

#### Kebutuhan Sistem :
- Webserver (Apache atau nginx)
- MySQL >5.7.8 / MariaDB 10.2 / Lychee's inbuilt SQLite3 support
- PHP >= 7.4 with various extension.
- RAM minimal 512 MB
- Hard Disk Space minimal 25 GB
- CPU minimal 2Ghz Dual Processor

#### Proses Instalasi :
1. Login ke server dengan username dan password masing masing

2. Install dan update kebutuhan sistem seperti `Apache`, `PHP`, dan `MySQL`.
   ```
    $ sudo apt-get update
    $ sudo apt-get install apache2
    $ sudo apt-get install mysql-server
    $ sudo apt-get install php
    $ sudo apt-get install libapache2-mod-php
    $ sudo apt-get install php-mysql
    $ sudo apt-get install openssl php-common php-curl php-json php-mbstring php-mysql php-xml php-zip php-tokenizer php-gd php-imagick
    $ dpkg --list | grep php
   ```
3. Install Lychee dengan menggunakan `Composer`
   ```
    $ sudo apt-get install git
    $ sudo apt-get install composer
    $ sudo chmod 777 /var/www/html
    $ git clone https://www.github.com/LycheeOrg/Lychee /var/www/html/Lychee
    $ cd /var/www/html/Lychee
    $ composer install --no-dev
    $ sudo chown -R www-data:www-data /var/www/html/Lychee
    $ sudo chmod -R 775 /var/www/html/Lychee

   ```
4. File konfigurasi `Apache`.
   - Menghapus konfigurasi default
     ```
      $ sudo rm /etc/apache2/sites-available/000-default.conf
      $ sudo rm /etc/apache2/sites-enabled/000-default.conf
     ```
   - Membuat konfigurasi baru untuk lychee
     ```
      $ sudo a2enmod rewrite
      $ sudo touch /etc/apache2/sites-available/lychee.conf
      $ sudo nano /etc/apache2/sites-available/lychee.conf
     ```
 5. Pada konfigurasi `Apache` baru yang terbuka, isikan konfigurasi sebagai berikut
     ```
     <VirtualHost *:80>
      ServerAdmin admin@your-domain.com
      DocumentRoot /var/www/html/Lychee/public
      ServerName your-domain.com
      ServerAlias www.your-domain.com
      <Directory /var/www/html/Lychee/>
      Options FollowSymLinks
      AllowOverride All
      Order allow,deny
      allow from all
      </Directory>
      ErrorLog /var/log/apache2/your-domain.com-error_log
      CustomLog /var/log/apache2/your-domain.com-access_log common
      </VirtualHost>
     ```
 6. Mennyalakan site `Apache`.
     ```
      $ sudo a2ensite lychee.conf (pada directory /var/www/html/)
     ```
 7. Merestart `Apache`.
     ```
      $ sudo service apache2 restart
     ```
 8. Mengecek IP Adress komputer.
     ```
      $ hostname -I
     ```
 9. Instalasi lanjutan 
      - Welcome to **Lychee**
        ![Screenshot (14)](https://user-images.githubusercontent.com/60083608/111331720-c4887300-86a3-11eb-97f9-0442e0b4d57a.png)
      - Mengecek kelengkapan `Apache` dan `PHP`.
        ![Screenshot (109)](https://user-images.githubusercontent.com/60083608/111331954-f6013e80-86a3-11eb-9247-b5263acac979.png)
        ![Screenshot (116)](https://user-images.githubusercontent.com/60083608/111331961-f8639880-86a3-11eb-9b1b-e740f8126e78.png)
      - Mengecek *Permission*
        ![Screenshot (222)](https://user-images.githubusercontent.com/60083608/111332301-3d87ca80-86a4-11eb-9d3e-621864999235.png)
        ![Screenshot (223)](https://user-images.githubusercontent.com/60083608/111332311-41b3e800-86a4-11eb-814a-6714f62c2daa.png)
      - Membuat database dan mengedit konfigurasi
        ![Screenshot (224)](https://user-images.githubusercontent.com/60083608/111332862-bb4bd600-86a4-11eb-9859-150effa5d914.png)
        ![Screenshot (225)](https://user-images.githubusercontent.com/60083608/111332868-bd159980-86a4-11eb-9618-f6d816053ba4.png)
        ![Screenshot (226)](https://user-images.githubusercontent.com/60083608/111332874-be46c680-86a4-11eb-9c12-943a47e421ed.png)
        ![Screenshot (227)](https://user-images.githubusercontent.com/60083608/111332879-bf77f380-86a4-11eb-898c-ffcc6237934a.png)
         ```
            $ sudo mysql -u root -p -v -e "
               CREATE DATABASE lychee;
               CREATE USER 'lycheeuser'@'localhost' IDENTIFIED BY 'lycheepassword';
               GRANT ALL PRIVILEGES ON lychee.* TO 'lycheeuser'@'localhost';
               FLUSH PRIVILEGES;"
               
            DB_CONNECTION=mysql
            DB_HOST=localhost
            DB_PORT=3306
            DB_DATABASE=lychee
            DB_USERNAME=lycheeuser
            DB_PASSWORD=lycheepassword
            DB_LOG_SQL=false
         ```
       - Jika berhasil maka muncul status "Application key set successfully"
         ![Screenshot (342)](https://user-images.githubusercontent.com/60083608/111333416-42994980-86a5-11eb-9059-9f940446369d.png)
         

# Konfigurasi
[`^ kembali ke atas ^`](#)
1. Pengaturan *Sorting* dan *Dropbox key* untuk menghubungkan ke *Dropbox*

<img src="img/config1.png"/>

2. Pengaturan *Layout*

<img src="img/config2.png"/>

3. Pengaturan *Image Overlay*

<img src="img/config3.png"/>
<img src="img/config4.png"/>

4. Pengaturan lokasi foto

<img src="img/config5.png"/>

5. Pengaturan *Visibility* dan CSS 

<img src="img/config6.png"/>



# Maintenance
[`^ kembali ke atas ^`](#)
* ### Logs
![Screenshot (779)](https://user-images.githubusercontent.com/48718969/111182496-89257000-85e1-11eb-9167-77f697157ded.png)
* ### Diagnostic
![Screenshot (780)](https://user-images.githubusercontent.com/48718969/111182608-a65a3e80-85e1-11eb-83c3-8ade044804cc.png)

![Screenshot (781)](https://user-images.githubusercontent.com/48718969/111182629-ac501f80-85e1-11eb-9a5b-85f81c26183f.png)



# Otomatisasi
[`^ kembali ke atas ^`](#)




# Cara Pemakaian
[`^ kembali ke atas ^`](#)
* ### Import from link 
1. 
![Screenshot (446)](https://user-images.githubusercontent.com/48718969/111315843-589f0e00-8695-11eb-845f-fe30ab56c0f5.png)
2. 
![Screenshot (700)](https://user-images.githubusercontent.com/48718969/111315899-63f23980-8695-11eb-9de6-f549a31d9374.png)
3. 
![Screenshot (717)](https://user-images.githubusercontent.com/48718969/111315994-77050980-8695-11eb-8cfe-d5095e30531f.png)
* ### Favorite
![favorite](https://user-images.githubusercontent.com/48718969/111183599-a870cd00-85e2-11eb-8822-452ccb1ca2bb.JPG)
* ### Move 
![move](https://user-images.githubusercontent.com/48718969/111183671-bd4d6080-85e2-11eb-92e2-57f9934f7bf2.png)
* ### Rotate
1.
![rotate](https://user-images.githubusercontent.com/48718969/111183805-e3730080-85e2-11eb-9f47-be64b83137a9.JPG)
2. 
![Screenshot (758)](https://user-images.githubusercontent.com/48718969/111311135-6e5e0480-8690-11eb-8a91-06f5e546ce34.png)
* ### About
![Screenshot (520)](https://user-images.githubusercontent.com/48718969/111316308-bc293b80-8695-11eb-8c5e-4db20f77ec9b.png)
* ### Delete photo
![Screenshot (695)](https://user-images.githubusercontent.com/48718969/111316511-e975e980-8695-11eb-89be-b7388b63a433.png)
* ### Visibility
![Screenshot (741)](https://user-images.githubusercontent.com/48718969/111317107-6c973f80-8696-11eb-9291-76e0607068a1.png)

![Screenshot (742)](https://user-images.githubusercontent.com/48718969/111317140-71f48a00-8696-11eb-92ca-9008cd8e3a59.png)
* ### Share photo
![Screenshot (759)](https://user-images.githubusercontent.com/48718969/111317338-a405ec00-8696-11eb-8327-b507faf8b1c3.png)
* ### Photo View 
![Screenshot (760)](https://user-images.githubusercontent.com/48718969/111317764-06f78300-8697-11eb-884f-6637446e2603.png)







# Pembahasan
[`^ kembali ke atas ^`](#)

Software management foto ini memberikan banyak fitur bermanfaat untuk pengelolaan foto. 
Memberikan akses kepada pengguna untuk membuat repository foto untuk server websitenya.


# Referensi
[`^ kembali ke atas ^`](#)


1. [How to install Lychee on Ubuntu 16.04](https://www.youtube.com/watch?v=MpkJCrRfVCQ) - Youtube
2. [Cara Install Ubuntu Server 18.04 LTS pada Virtual Machine](https://degananda.com/cara-install-ubuntu-server-18-04-lts-pada-virtual-machine/) - degananda.com
3. [Lychee Prologue](https://lycheeorg.github.io/docs/org.html) - Github
