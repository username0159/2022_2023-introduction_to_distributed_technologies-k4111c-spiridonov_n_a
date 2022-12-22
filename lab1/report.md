### University: [ITMO University](https://itmo.ru/ru/)
### Course: [Introduction to distributed technologies](https://github.com/itmo-ict-faculty/introduction-to-distributed-technologies)
### Year: 2022/2023
### Group: K4111c
### Author: Spiridonov Nikita Andreevich
### Date of create: 20.09.2022
### Date of finished:
---

Предварительно по инструкции мы установили докер.

Далее пишем следующий манифест с помощью которого мы развернем наш деплоймент с одним подом
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

Создаем сервис доступа 
```
minikube kubectl -- expose pod <èìÿ ïîäà> --type=NodePort --port=8200
```

Прокидываем порт к контейнеру
```
minikube kubectl -- port-forward service/<èìÿ ïîäà> 8200:8200
```
По ссылке [http://localhost:8200](http://localhost:8200) обнаружим следующий интерфейс
![Image alt](https://github.com/username0159/2022_2023-introduction_to_distributed_technologies-k4111c-spiridonov_n_a/blob/main/lab1/voult1.jpg)

Открываем логи
```
 kubectl logs -f <èìÿ ïîäà>
```
Ищем строчку root token и вводим в нужное поле
![Image alt](https://github.com/username0159/raw/blob/main/voult.jpg)

Готово

---

![Image alt](https://github.com/username0159/2022_2023-introduction_to_distributed_technologies-k4111c-spiridonov_n_a/blob/main/l1..JPG)
