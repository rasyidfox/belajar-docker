# Cara Upload Image Local Menuju Registry

login menuju Registry 

```bash
> docker login <username>
```

Ubah nama local image 

```bash
> docker tag <local-image:tagname> <repo-name:tagname>
```

Setelah diubah push menuju registry

```bash
> docker push <repo-name:tagname>
```
