# Belajar Docker Dasar

### Docker Image
Untuk melihat Docker Image dalam Docker Daemon

``` bash
> docker image ls
> docker images
```
Mendowload Docker Image dari Docker Registry 

``` bash
> docker image pull <namaimage:tags>
```
Menghapus Docker Image dari Local Registry

``` bash
> docker image rm <namaimage:tags>
```

### Docker Container

Membuat container 

```bash
> docker container create --name <nama-container> <namaimage:tags>
```

Melihat semua container
```bash
> docker container ls -a
```

Melihat container yang sedang berjalan 
```bash
> docker container ls
```

Menjalankan container
```bash
> docker container start <nama-container>
```

Menghentikan container

```bash
> docker container stop <nama-container>
```

Menghapus container

```bash
> docker container rm <nama-container>
```
#### Container Log

Melihat Container Log

```bash
> docker container logs <nama-container>
```

Melihat Container Log Secara Real Time

```bash
> docker container logs -f <nama-container>
```

#### Container Exec

Masuk menuju shell yang ada pada container

```bash
> docker container exec -i -t <nama-container> /bin/bash
```

* -i : Interaktif, berguna agar menjaga input tetap aktif

* -t : alokasi Pseudo-TTY (Terminal Akses)

* /bin/bash atau /bin/sh salah satu kode program yang ada pada container

#### Container Port

Melakukan Port Forwarding pada Docker Container

```bash
> docker container create --name <nama-container> --publish/-p <port-host>:<port-container> <namaimage:tags>
```

#### Container Environment Variable

Menambahkan Environment Variable

```bash
> docker container create --name <nama-container> --publish/-p <port-host>:<port-container> --env/-e <KEY:value> <namaimage:tags>
```

Jika Environment Variable lebih dari satu sesuaikan contoh :

```bash
> docker container create --name <nama-container> --publish/-p <port-host>:<port-container> --env/-e <KEY:value> <namaimage:tags>
 --env/-e <KEY2:value>
```

#### Container Stats

Melihat penggunaan sumber daya pada Docker Container yang berjalan
```bash
> docker container stats
```

#### Container Resource Limit

Memberikan limitasi sumber daya pada Container menggunakan --memory dan --cpus
```bash
> docker container --name <nama-container> --publish/-p <port-host>:<port-container> --memory <100b(bytes)/k(killobytes)/m(megabytes)/g(gigabytes)> --cpus <limitasi-cpu> <namaimage:tags>
```
### Bind Mount

Bind Mounts merupakan kemampuan melakukan mounting (sharing) file atau folder yang terdapat di sistem host ke container yang terdapat pada docker, fitur ini berguna ketika kita ingin mengirim konfigurasi dari luar container, atau misal menyimpan data yang dibuat di aplikasi di dalam container ke dalam folder di sistem host, jika file atau folder tidak ada di sistem host, secara otomatis akan dibuatkan oleh Docker, untuk melakukan mounting, kita bisa menggunakan parameter --mount ketika membuat container, isi dari parameter --mount memiliki aturan tersendiri 

#### Parameter Mount

| Parameter     | Keterangan                               |
| ------------- | ---------------------------------------- |
| `type`        | Tipe Mount, bind atau volume             |    
| `source`      | Lokasi file atau folder di sistem host   |
| `destination` | Lokasi file atau folder di container     |
| `readonly`    | Jika ada, maka file aatau folder hanya bisa dibaca di container, tidak bisa ditulis|
### [Cara upload Local Image to Registry](Upload-Image-To-Registry.md)

Referensi :
[Programmer Zaman Now - Slide Docker Dasar](https://www.youtube.com/watch?v=3_yxVjV88Zk&t=5336s&ab_channel=ProgrammerZamanNow)
