# Membuat Image pada Local Registry

Buatlah dockerfile terlebih dahulu, setelah membuat dockerfile letakkan dockerfile pada folder yang sama dengan project yang ingin dibuat image setelah itu build

```bash
docker build <tempat projek dan dockerfile> --tag <tag>
```
Lalu cek image untuk memastikan bahwa image telah dibuat 

```bash
docker image ls
```
