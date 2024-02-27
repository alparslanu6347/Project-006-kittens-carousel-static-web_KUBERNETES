# Step by step prepare project

- Worker-node'a git

- Worker-node içerisinde `kittens-local-volume` isimli klasör oluştur ==>> `PersistentVolume`  tanımlarken "hostPath" olarak belirteceğiz. Bu klasörü oluşturmasan da `PersistentVolume` tanımlarken bu klasör kendisi oluşacak.

- Master-node'a git

```bash (pwd : home/ubuntu)
mkdir Lesson
cd Lesson
```
  
- Master-node içerisinde çalışacağın klasör yapısı aşağıdaki gibi olsun :

    ├── kittens-deploy.yaml
    ├── kittens-service.yaml
    ├── kittens-pv.yaml
    ├── kittens-pvc.yaml
    ├── commands.md
    ├── Dockerfile
    └── static-web (klasör)
        ├── cat0.jpg
        ├── cat1.jpg
        ├── cat2.jpg
        └── index.html

- `Dockerfile` oluşturalım , image oluşturalım , dockerhub'a push edelim.

```bash
touch Dockerfile

    # FROM ubuntu
    # RUN apt-get update -y
    # RUN apt-get install python3 -y
    # RUN apt-get install python3-pip -y
    # RUN pip3 install flask
    # COPY . /app
    # WORKDIR /app
    # CMD python3 ./phone.py

docker build -t "alparslanu6347/kittens-flask:1.0" .        # alparslanu6347 : dockerhub username
docker login # username: alparslanu6347  , password: **********
docker alparslanu6347/kittens-flask:1.0
```

- Dockerhub hesabımda bulunan image'i (yukarıda oluşturduğum) kullanarak Kubernetes ile uygulamayı çalıştıralım.

```bash
kubectl apply -f .
kubectl get ns,po,svc,deploy,pv,pvc
http://[public-node-ip]:[node-port] # http://54.127.45.88:30333  (nodePort: 30333)
kubectl delete -f .
```
