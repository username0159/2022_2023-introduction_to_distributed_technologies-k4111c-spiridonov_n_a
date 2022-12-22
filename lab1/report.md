### University: [ITMO University](https://itmo.ru/ru/)
### Course: [Introduction to distributed technologies](https://github.com/itmo-ict-faculty/introduction-to-distributed-technologies)
### Year: 2022/2023
### Group: K4111c
### Author: Spiridonov Nikita Andreevich
### Date of create: 20.09.2022
### Date of finished:
---
Разворачиваем следующий деплоймент
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: lab1
  labels:
    app: vault
spec:
  replicas: 1
  selector:
    matchLabels:
      app: vault
  template:
    metadata:
      labels:
        app: vault
    spec:
      containers:
      - name: vault
        image: username0159/lab1_vault:latest
        ports:
        - containerPort: 8200
```

Создаем сервис
```
minikube kubectl -- expose pod <èìÿ ïîäà> --type=NodePort --port=8200
```

Прокидываем порт
```
minikube kubectl -- port-forward service/<èìÿ ïîäà> 8200:8200
```

В логах ищем строчку root token и вводим в нужное поле
```
 kubectl logs -f <èìÿ ïîäà>
```
![Image alt](https://github.com/username0159/raw/blob/main/voult.jpg)
