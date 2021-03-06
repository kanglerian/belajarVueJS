# Memulai Kelas

Selamat datang di kelas Belajar Vue JS. Disini kita akan belajar Vue basic, sampai kita bisa membuat Website sederhana menggunakan Vue JS 😄
Website ini adalah dokumentasi dari hasil belajar dari berbagai sumber mengenai Vue JS, jadi untuk beberapa kesalahan mohon dimaafkan dan boleh dikoreksi, oke?

Let's Started! 😄

<hr>

# Instalasi Vue JS

1. **Install NPM**<br>
   Untuk mendapatkan NPM bisa kita download di link ini : [https://www.npmjs.com/get-npm](https://www.npmjs.com/get-npm)<br>
   Untuk menginstallnya, buka terlebih dahulu terminal kalian atau jika menggunakan OS Windows, bisa pakai Git Bash.

   ```Shell
   $ sudo apt-get update
   $ sudo apt-get install npm
   $ npm -v //untuk cek versi npm
   ```

2. **Install Vue**<br>
   Untuk mendapatkan Vue bisa kita download di link ini : [https://vuejs.org/v2/guide/installation.html#NPM](https://vuejs.org/v2/guide/installation.html#NPM)<br>
   Untuk menginstallnya, buka terlebih dahulu terminal kalian atau jika menggunakan OS Windows, bisa pakai Git Bash.

   ```Shell
   $ npm install vue
   ```

3. **Install Vue CLI**<br>
   Untuk mendapatkan Vue CLI bisa kita download di link ini : [https://cli.vuejs.org/guide/installation.html](https://cli.vuejs.org/guide/installation.html)<br>
   Untuk menginstallnya, buka terlebih dahulu terminal kalian atau jika menggunakan OS Windows, bisa pakai Git Bash.

   ```Shell
   $ npm install -g @vue/cli
   ```

4. **Install Vue UI**<br>
   Untuk mendapatkan Vue UI bisa kita lakukan seperti ini.<br>
   Untuk menginstallnya, buka terlebih dahulu terminal kalian atau jika menggunakan OS Windows, bisa pakai Git Bash.

   ```Shell
   $ vue ui
   ```

   Jika perintahnya tidak bekerja, atau not command. Maka, jalankan ini terlebih dahulu `source ~/.bash_profile`

<hr>

# Membuat Project

Setelah toolsnya kita install, langsung saja untuk membuat project. Bisa kita buat di `vue ui` atau bisa kita buat di `terminal`. Saat ini, saya akan membuatnya di terminal

1. **Buat project dengan perintah**<br>
   `vue create hello-world`
2. **Run aplikasi** <br>
   Bisa kita run di `terminal` atau di Vue UI. Kali ini saya akan menjalankan project `Hello-World` di vue ui.

   - **Pilih import**

     ![Vue Images](/images/vue-images-1.png)

   - **Pilih Task**

     ![Vue Images](/images/vue-images-2.png)

   - **Pilih serve -> run task -> Open App**

     ![Vue Images](/images/vue-images-3.png)

   - **Berhasil! App Hello-World sudah selesai dibuat**

     ![Vue Images](/images/vue-images-4.png)

<hr>

# Deployment ke Github Pages

Caranya lumayan agak sulit, namun sumber dari apa yang akan kita lakukan adalah di website resmi Vue CLI itu sendiri. Bisa kita cek di link ini [https://cli.vuejs.org/guide/deployment.html#pwa](https://cli.vuejs.org/guide/deployment.html#pwa)

Berangkat dari sana, kita akan coba bahas satu per satu.

1. **Siapkan aplikasi Vue JS**
2. **Buat repository di Github**

- **Buat repository seperti ini `hello-world`**

  ![Vue Images](/images/vue-images-5.png)

- **Dan biarkan dulu seperti ini**

  ![Vue Images](/images/vue-images-6.png)

- **Uncomment `.gitignore` untuk /dist**

  ![Vue Images](/images/vue-images-7.png)

3. **Push ke Repository Githubmu**

   ```Shell
   $ git init
   $ git add .
   $ git commit -m "first commit"
   $ git remote add origin https://github.com/<USERNAME>/<REPO>.git
   $ git push -u origin master
   ```

![Vue Images](/images/vue-images-8.png)

4.  **Buat `vue.config.js` di root project** <br>
    Sesudah membuat filenya, maka masukan script dibawah ini :

    ```JS
    module.exports = {
    publicPath: process.env.NODE_ENV === 'production'
     ? '/my-project/'
     : '/'
    }
    ```

    ![Vue Images](/images/vue-images-9.png)

    Note: ganti `my-project` dengan project yang kamu buat yaitu `hello-world`.

5.  **Buat `deploy.sh` di root project** <br>
    Sesudah membuat filenya, maka masukan script dibawah ini dan ganti <USERNAME> dan <REPO> nya dengan yang kamu miliki yaitu kalau disini `kanglerian` untuk <USERNAME> dan `hello-world` untuk <REPO> :

    ```Shell
    #!/usr/bin/env sh

    # abort on errors
    set -e

    # build
    npm run build

    # navigate into the build output directory
    cd dist

    # if you are deploying to a custom domain
    # echo 'www.example.com' > CNAME

    git init
    git add -A
    git commit -m 'deploy'

    # if you are deploying to https://<USERNAME>.github.io
    # git push -f git@github.com:<USERNAME>/<USERNAME>.github.io.git master

    # if you are deploying to https://<USERNAME>.github.io/<REPO>
    git push -f git@github.com:<USERNAME>/<REPO>.git master:gh-pages

    cd -
    ```

    ![Vue Images](/images/vue-images-10.png)

6.  **Buat `deployment script` di `package.json`** <br>
    Tambahkan di "script" script dibawah ini:

    ```Shell
       "deploy" : "sh deploy.sh"
    ```

    ![Vue Images](/images/vue-images-10.png)

7.  **Push ke Github repository `hello-world`** <br>

    ```Shell
    $ git add .
    $ git commit -m "upload deploy script"
    $ git push
    ```

8.  **Coba jalankan deploy**<br>

    ```Shell
    $ npm run deploy
    ```

    > Jika ada pesan error yang bertuliskan "Permission denied (publickey).fatal: Could not read from remote repository," maka kamu harus atur SSH Key dan tambahkan di Github Account.

    maka ikuti cara-cara ini :

    - **Generating a new SSH**<br>

      1. Buka Terminal
      2. Ketik script ini di terminal

         ```Shell
         $ ssh-keygen -t ed25519 -C "your_email@example.com"
         ```

      3. Kemudian press[ENTER] dan ketikan password atau `passphare`

    - **Cek SSH mu dengan menggunakan** <br>

      ```Shell
         $ ls -al ~/.ssh
      ```

      > nanti akan keluar 3 ini `id_rsa.pub` `id_ecdsa.pub` `id_ed25519.pub`

    - **Tambahkan SSH mu ke SSH Agent** <br>

          ```Shell
             eval "$(ssh-agent -s)"
          ```

    - **Tambahkan ke Github Account mu** <br>
      Install xclip dibawah ini :

      ```Shell
      $ sudo apt-get install xclip
      $ xclip -selection clipboard < ~/.ssh/id_ed25519.pub
      ```

    - **Masuk ke Github Account `Setting` `SSH and GPG keys`**
    - **Pilih `New SSH key`**

    ![Vue Images](/images/vue-images-11.png)

    - **Isi Titlenya, contoh : Personal Linux**
    - **Simpan (paste) key tadi ke `key`**
    - **Klik add SSH Key**

9.  **Coba jalankan `deploy` sekali lagi** <br>

    ```Shell
    $ npm run deploy
    ```

10. **Berhasil!** <br>
    Selamat, kita sudah bisa deploy aplikasi Vue JS kita ke Github Pages

    ![Vue Images](/images/vue-images-12.png)
