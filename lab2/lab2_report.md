### University: [ITMO University](https://itmo.ru/ru/)
### Course: [Introduction to distributed technologies](https://github.com/itmo-ict-faculty/introduction-to-distributed-technologies)
### Year: 2022/2023
### Group: K4111c
### Author: Spiridonov Nikita Andreevich
### Date of create: 20.09.2022
### Date of finished:
---
Пишем манифест с помощью которого развернем наш деплоймент с 2 подами
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: lab2
  labels:
    app: lab2
spec:
  replicas: 2
  selector:
    matchLabels:
      app: lab2
  template:
    metadata:
      labels:
        app: lab2
    spec:
      containers:
      - name: lab2
        image: ifilyaninitmo/itdt-contained-frontend:master
        ports:
        - containerPort: 3000
        env:
          - name: REACT_APP_USERNAME
            valueFrom:
              configMapKeyRef:
                name: cm-lab2
                key: REACT_APP_USERNAME
          - name: REACT_APP_COMPANY_NAME
            valueFrom:
              configMapKeyRef:
                name: cm-lab2
                key: REACT_APP_COMPANY_NAME
```

Сервис Load Balancer который бедет контролировать трафик
```
apiVersion: v1
kind: Service              
metadata:
  name: serv-lab2
spec:
  type: LoadBalancer       
  ports:
  - port: 3000
    protocol: TCP          
    targetPort: 3000
  selector:                
    app: lab2       
```

Без подачи переменных мы видим следующее
![Image alt](https://github.com/username0159/2022_2023-introduction_to_distributed_technologies-k4111c-spiridonov_n_a/blob/main/lab2/lab2-1.jpg)

Конфиг мэп. Он нужен нам для задания переменных
```
apiVersion: v1
kind: ConfigMap
metadata:
  name: cm-lab2
data:
    REACT_APP_USERNAME: Hi, my nickname should be here
    REACT_APP_COMPANY_NAME: and my company name
```

Смотрим что изменилось
```
minikube service serv-lab2
```
![Image alt](https://github.com/username0159/2022_2023-introduction_to_distributed_technologies-k4111c-spiridonov_n_a/blob/main/lab2/lab2-2.jpg)

Теперь в поля username и company name мы видим то что было указано в config файле. Так же изменилось имя пода благодаря нашему Load Balancer'у
