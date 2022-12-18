# TUBES MRV
penjelasan singkat tentang project tugas besar kelompok kami. yang mana kami beranggotakan 6 orang yaitu
1.Nasrul Alfin      (121140001)
2.Fauzan            (121140009)
3.Annisa Checilia   (121140047)
4.Novi fitria       (121140078)
5.Heni Artha        (121140080)
6.Rahmat Fadhil     (121140109)

(https://replit.com/@109Rahmat-Fadhi/Tubes-MRV#main.py)



Ditugas besar kali ini, kami mengangkat tentang permasalahan sistem persamaan linear dengan metode gaus, dan gaus-jordan. yang mana program kami akan membantu setiap persoalan tentang sistem persamaan linear dengan tiga solusi. adapun solusi di program kami antara lain:
1. solusi unik (tunggal)
2. banyak solusi (tak terhingga)
3. tidak ada solusi

## Dua inti program
program kami memiliki dua inti program yang pertama program yang membuat rumus gaus, dan yang kedua program yang membuat rumus gaus jordan.

adapun program gaus sebagai berikut:

```sh
def gauss(matriks, baris, kolom, i=0, z=0):
  # tujuan : memproses matriks dengan metode eleminasi gauss
  # jika i dan z sesuai dengan syarat posisi matriks
  if i < baris:
    if z < kolom - 1:
      # jika nilai suku matriks = 0, maka sorting dengan yang memiliki angka
      if matriks[i][z] == 0:
        for j in range(i + 1, baris):
          # jika angka atau bukan nol, maka "tukar"
          if matriks[j][z] != 0:
            for k in range(kolom):
              # "tukar" = seluruh baris matriks 1 dengan yang lain
              matriks[i][k], matriks[j][k] = matriks[j][k], matriks[i][k]
            # menampilkan info proses sistem penukaran
            tampilMatriks(matriks, baris, kolom)
            break
      # setelah sorting, jika suku matriks != 0, maka "cek satu" dan "buat satu"
      if matriks[i][z] != 0:
        # jika matriks tidak 1, maka "eliminasi jadi satu"
        if matriks[i][z] != 1:
          # "eliminasi jadi satu"
          temp = matriks[i][z]
          for j in range(z, kolom):
            matriks[i][j] /= temp
          # manmpilkan info sistem eliminasi jadi satu
          tampilMatriks(matriks, baris, kolom)
        # "buat satu" -> membuat hanya ada satu nilai dalam satu kolom
        for j in range(i + 1, baris):
          if matriks[j][z] != 0:
            # jika matriks tidak nol, maka lakukan eliminasi dengan matriks yang bernilai awal 1
            temp = matriks[j][z] / matriks[i][z]
            for k in range(z, kolom):
              matriks[j][k] = matriks[j][k] - \
                  (temp * matriks[i][k])
            # menampilkan info sistem eliminasi agar satu nilai dalam satu kolom
            tampilMatriks(matriks, baris, kolom)

        # jika proses "sorting", eliminasi "jadi satu" dan "buat satu" selesai,
        # maka panggil function "gauss" kembali dengan nilai i yang bertambah
        i += 1
        gauss(matriks, baris, kolom, i, z)
      else:
        # jika matriks = 0, maka panggil function "gauss" dengan nilai z bertambah
        z += 1
        gauss(matriks, baris, kolom, i, z)
```

sedangkan program gaus jordan sebagai berikut:

```sh
def jordan(matriks, baris, kolom, aljabar):
  # tujuan : melakukan proses jordan saja pada konsep eliminasi gauss-jordan
  # dibawah ini proses pengecekan apakah dia solusi unik, banyak dan tidak ada solusi
  unik = False
  for i in range(baris):
    cekIsi = True
    cekHasil = False
    for j in range(kolom):
      if j < kolom - 1:
        if matriks[i][j] == 0 and cekIsi == True:
          cekIsi = True
        else:
          cekIsi = False
      else:
        if matriks[i][j] == 0:
          cekHasil = True
        else:
          cekHasil = False

    # jika isi baris matriks bernilai 0 dan hasil baris matriks bernilai !0, maka tidak ada sulusi
    if cekIsi == True and cekHasil == False:
      print(" ")
      print(
        "Sistem Persamaan Linear tersebut memiliki : Tidak Ada Solusi".center(
          48))
      break
    # jika isi baris matriks bernilai 0 dan hasil baris matriks bernilai 0 juga, maka banyak solusi
    elif cekIsi == True and cekHasil == True:
      solusi = " Sistem Persamaan Linear tersebut memiliki : Banyak Solusi"

      break
  # jika bukan (tidak ada solusi dan banyak solusi), maka solusi unik
  else:
    solusi = "Sistem Persamaan Linear tersebut memiliki : Solusi Unik"
    unik = True

  if unik == True or (cekIsi == True and cekHasil == True):
    # perulangan dimulai dari paling bawah (cek yang bawah terlebih dahulu)
    for i in range(baris - 1, -1, -1):
      for j in range(kolom - 1):
        # jika nilai matriks !0, maka eliminasi matriks diatasnya yang sejajar
        if matriks[i][j] != 0:
          for k in range(i - 1, -1, -1):
            # proses eliminasi matriks diatasnya yang sejajar
            if matriks[k][j] != 0:
              temp = matriks[k][j] / matriks[i][j]
              for l in range(j, kolom):
                matriks[k][l] -= (temp * matriks[i][l])
              # menampilkan info sistem eliminasi yang dilakukan
              tampilMatriks(matriks, baris, kolom)
          break
    print(" ")
    print(" " + solusi.center(48) + " ")
    print(" ")
    # setelah eliminasi "jordan", maka mengeluarkan hasil dari setiap variabel
    for i in range(baris):
      cek = False
      for j in range(kolom):
        if matriks[i][j] != 0 and j < kolom - 1:
          if cek == True:
            print(" +", end="")
          print(" {}{}".format(matriks[i][j], aljabar[j]), end="")
          cek = True
      if cek == True:
        print(" = {}".format(matriks[i][j]))
  print(" ")

```

## penjelasan singkat
diprogram kami memiliki 3 pilihan menu antara lain:
1. menu penyelesaian sistem persamaan linear
2. menu menampilkan nama anggota
3. menu berhenti

dimenu pertama anda akan memiliki dua buah pilihan yang mana pilihan tersebut adalah 
A. memilih untuk menginputkan spl secara manual
di menu ini anda akan disuguhkan untuk mengisi variable sesuai yang anda minta, jika anda memilih tidak maka variable akan otomatis terisi oleh (x).
B. memilih untuk melakukan inputan secara interval
jika anda memilih memasukan secara interval maka anda akan disuguhkan dengan Rumus : 
```sh
nx^m / oy^p 
```
yang mana input an nya mengikuti variable sebagai berikut:
```sh
 Input -999 = var akan mengikuti nilai interval
 ```
 
 jika anda memilih menu menampilkan nama anggota maka program akan lansung mengeluarkan nama anggota kelompok kami, contoh output nya:
 ```sh
 ---------------    Tubes MRV RC    ---------------
 
---------------  Anggota Kelompok  ---------------
 
Nama : Nasrul Alfin Prassetyo                   
NIM  : 121140001                                
 
Nama : FAUZAN                                   
NIM  : 121140009                                
 
Nama : Annisa Checilia Astuti                   
NIM  : 121140047                                
 
Nama : Novi Fitria Ramadhan                     
NIM  : 121140078                                
 
Nama : Heni Artha Uli br. Turnip                
NIM  : 121140080                                
 
Nama : Rahmat Fadhil Syauqy.A                   
NIM  : 121140109                                
--------------------------------------------------
 ```
 
 dan jika anda memilih menu berhenti maka program otomatis akan berhenti.


