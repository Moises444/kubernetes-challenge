# Steps taken to do the challenge on GCP
### 1. Went into to the Docker file and changed name to Moises.

From:
```javascript
res.send(`Hello ${name}!`);
```

To: 
```javascript
res.send('Hello Moises')
```
---
### 2. Cloned the repository in the cloud shell

> git clone https://github.com/learnk8s/kubernetes-challenge.git
---
### 3. Created the Docker image. 
> $ ls 
kubernetes-challenge  README-cloudshell.txt

> $ cd kubernetes-challenge
moisesasaldana@cloudshell:~/kubernetes-challenge (gentle-impulse-327504)$

> $ docker build . -t donatello
> 
> $ docker tag donatello gcr.io/gentle-impulse-327504/donatello
---
 
### 4. I need to push it to the registry. Once i made the image I needed to tag it. 


> $ docker push gcr.io/gentle-impulse-327504/donatello
---
### 5. Now to do the fun stuff. 
> $ cd .. 
from  moisesasaldana@cloudshell:~/kubernetes-challenge (gentle-impulse-327504)$
to   moisesasaldana@cloudshell:~ (gentle-impulse-327504)$

> $ gcloud config set project gentle-impulse-327504

> $ gcloud config set compute/zone us-central1-a

> $ gcloud container clusters create cluster-1 --num-nodes=1

> $ gcloud container clusters get-credentials cluster-1

> $ kubectl create deployment web-server-1 --image=gcr.io/gentle-impulse-327504/donatello@sha256:d577258ac2ba6d01440890507d5d5a06e0a6f1daf93739faa8c64690ef66be87

> $ kubectl expose deployment web-server-1 --type LoadBalancer --port 80 --target-port 80
---
### 6. Now its the moment of truth!!
> $ kubectl get service

![Screenshot 2021-09-29 222134](https://user-images.githubusercontent.com/90883758/135574708-4c4f313a-7961-4d90-87fc-63f7c4659bc6.jpg)


---
### 7. One last thing.
> $ curl 34.134.205.168

![Screenshot 2021-09-29 222307](https://user-images.githubusercontent.com/90883758/135574687-8cfc9f3e-de91-45fa-8a3d-5cc185e261de.jpg)
IT WORKS!!!



