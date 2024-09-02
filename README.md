# Домашнее задание к занятию «Базовые объекты K8S»

### Инструменты и дополнительные материалы, которые пригодятся для выполнения задания

1. Описание [Pod](https://kubernetes.io/docs/concepts/workloads/pods/) и примеры манифестов.
2. Описание [Service](https://kubernetes.io/docs/concepts/services-networking/service/).

------

### Задание 1. Создать Pod с именем hello-world

1. Создать манифест (yaml-конфигурацию) Pod.
2. Использовать image - gcr.io/kubernetes-e2e-test-images/echoserver:2.2.
3. Подключиться локально к Pod с помощью `kubectl port-forward` и вывести значение (curl или в браузере).

### Ответ 
Манифест: https://github.com/otuzi/base-objects-k8s/blob/main/hello-world-pod.yaml 

```
ubuntu@fhm3m3re0r8c9vm9e395:~/k8s-manifests$ kubectl apply -f hello-world-pod.yaml
pod/hello-world created
ubuntu@fhm3m3re0r8c9vm9e395:~/k8s-manifests$ 
ubuntu@fhm3m3re0r8c9vm9e395:~/k8s-manifests$ 
ubuntu@fhm3m3re0r8c9vm9e395:~/k8s-manifests$ kubectl get pods
NAME          READY   STATUS              RESTARTS   AGE
hello-world   0/1     ContainerCreating   0          9s
ubuntu@fhm3m3re0r8c9vm9e395:~/k8s-manifests$ 
ubuntu@fhm3m3re0r8c9vm9e395:~/k8s-manifests$ 
ubuntu@fhm3m3re0r8c9vm9e395:~/k8s-manifests$ 
ubuntu@fhm3m3re0r8c9vm9e395:~/k8s-manifests$ kubectl get pods
NAME          READY   STATUS    RESTARTS   AGE
hello-world   1/1     Running   0          2m9s
ubuntu@fhm3m3re0r8c9vm9e395:~/k8s-manifests$ kubectl port-forward pod/hello-world 8080:8080
Forwarding from 127.0.0.1:8080 -> 8080
Forwarding from [::1]:8080 -> 8080
Handling connection for 8080
```

Так как я развернул VM c microk8s в yandex.cloud, то достучатся черз браузер до контейнера через port-forward нет возможности, надо сервис публикова. 
Но с подключением к VM по ssh, могу вывести вывод cutl http://localhost:8080/

```
ubuntu@fhm3m3re0r8c9vm9e395:~$ curl http://localhost:8080


Hostname: hello-world

Pod Information:
	-no pod information available-

Server values:
	server_version=nginx: 1.12.2 - lua: 10010

Request Information:
	client_address=127.0.0.1
	method=GET
	real path=/
	query=
	request_version=1.1
	request_scheme=http
	request_uri=http://localhost:8080/

Request Headers:
	accept=*/*
	host=localhost:8080
	user-agent=curl/7.68.0

Request Body:
	-no body in request-

ubuntu@fhm3m3re0r8c9vm9e395:~$
```
------

### Задание 2. Создать Service и подключить его к Pod

1. Создать Pod с именем netology-web.
2. Использовать image — gcr.io/kubernetes-e2e-test-images/echoserver:2.2.
3. Создать Service с именем netology-svc и подключить к netology-web.
4. Подключиться локально к Service с помощью `kubectl port-forward` и вывести значение (curl или в браузере).

------

### Правила приёма работы

1. Домашняя работа оформляется в своем Git-репозитории в файле README.md. Выполненное домашнее задание пришлите ссылкой на .md-файл в вашем репозитории.
2. Файл README.md должен содержать скриншоты вывода команд `kubectl get pods`, а также скриншот результата подключения.
3. Репозиторий должен содержать файлы манифестов и ссылки на них в файле README.md.

------
