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

Menghapus semua docker image dari local registry

```bash
> docker rmi $(docker images -q)
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
Menghapus semua container 

```bash
> docker container rm $(ps -aq )
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

Contoh bind mounting :

```bash
> docker container create --name <nama-container> --publish <port-host>:<port-container> --mount "type=bind,source=folder,destination=folder,readonly (Opsional)" <namaimage:tags>
```

### Docker Volume
Docker Volume berguna untuk menyimpan data apabila data dalam container dihapus data tidak hilang dan tetap ada pada volume

Membuat volume :

```bash
> docker volume create <nama-volume>
```

Melihat volume :

```bash
> docker volume ls
```
Menghapus volume :

```bash
> docker volume rm <nama-volume>
```

#### Container Volume
Volume yang sudah dibuat dapat digunakan dalam container. Volume sangat efektif ketimbang menggunakan bind mount, jika container dihapus, maka data akan tetap aman di volume. Cara menggunakan volume sama halnya dengan menggunakan bind-mount yaitu menggunakan ``--mount``
Contoh :

```bash
> docker container create --name <nama-container> --publish <port-host>:<port-container> --mount "type=volume,source=<nama-volume-yang-telah-dibuat>,destination=folder,readonly (Opsional)" <namaimage:tags>
```

#### Backup Volume

```bash
> docker container run --rm --name ubuntu --mount "type=bind,source=<folder-tempat-backup-local>,destination=<destinasi>" --mount "type=volume,source=<nama-volume>,destination=<destinasi>" ubuntu:latest tar cvf /<destinasi-bind>/backup.tar.gz /<destinasi-volume>
```

#### Restore Volume

```bash
> docker container run --rm --name ubuntu --mount "type=bind,source=<folder-tempat-backup-local>,destination=<destinasi>" --mount "type=volume,source=<nama-volume>,destination=<destinasi>" ubuntu:latest bash -c cd /<destinasi-volume> && tar xvf /destinasi-bind>/backup.tar.gz
```

### Docker Network

| Tipe          | Keterangan                               |
| ------------- | ---------------------------------------- |
| `bridge`      | Driver yang digunakan untuk membuat network secara virtual yang memungkinkan container yang terkoneksi di bridge network yang sama saling berkomunikasi   |    
| `host`        | Driver yang digunakan untuk membuat network yang sama dengan sistem host. host hanya jalan di Docker Linux, tidak bisa digunakan di Mac atau Windows |
| `none`        | Driver untuk membuat network yang tidak bisa berkomunikasi     |

Melihat Network :
```bash
> docker network ls
```
Membuat Network :

```bash
> docker network create --driver <bridge/host/none> <nama-network>
```

Menghapus Network :
```bash
> docker network rm <nama-network>
```
### Container Network
### Inspect
### Prune

#### [Membuat Image pada Local Registry](Image-Local-Registry.md)
#### [Upload Local Image menuju Registry](Upload-Image-To-Registry.md)
#### [Menjalankan Ubuntu pada Docker](Ubuntu-Docker.md)

## Referensi :
[Programmer Zaman Now](https://www.youtube.com/watch?v=3_yxVjV88Zk&t=5336s&ab_channel=ProgrammerZamanNow)

