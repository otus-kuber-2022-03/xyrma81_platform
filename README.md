# xyrma81_platform


## Kubernetes-Intro

- Развернут локальный кластер kubernetes посредством minikube
- Установлена актуальная версия kubectl
- Создан первый докерфайл с nginx
- Создан первый под web-pod.yaml
- Разобраны декларативный и императивный подходы


## Kubernetes-Intro

- Развернут кластер k8s посредством kind
- Произведено знакомство с контроллерами в k8s

## Kubernetes-Security

- Изучены возможно разграничения ролей в кластере, а так же создание неймспейсов
- Созданы необходимые неймспейсы
- Созданы необходимые пользователи с разными уровнями доступа

## Kubernetes-Networks

- Изучены возможности и ресурсы для сетевого взаимодействия pod.
- Подняты необходимые сервисы
- Развернут кластер minicube
- Включен ipvs
- Установлен metallb
- Ознакомлен с созданием ingress
- Ознакомлен с написанием сервисов clusterIP и loadbalancer
- Создан сервис типа loadbalancer для доступа к coredns снаружи minicube
- Открыт доступ к Dashboard через ingress
- Ознакомлен с canary release

### Проверка не валидна:

Данной командой мы проверяем работу процесса отвечающего за работу контейнера, и если он упадет, то контейнер будет перезапущен.

Подобная проверка может быть использована для проверки других процессов в контейнере

## kubernetes-Volumes

- Создан стейтфулсет с приложением minio
- Создан headless сервис
- Создан секрет
- Обновлен стейтфулсет для использлвания секрета

## Kubernetes-Templating

- Развернут кластер в yandex cloud
- Установлен helm 3
- Согласно инструкции установлен nginx-ingress с внешиним ip 51.250.108.240
- Установлен cert-manager, chartmusem, harbor
- Создан собственный helm chart и добавил в него файл из описания
- Отделены отдельные микросервисы из большого helm чарта
- Произведено ознокомление с kubecfg
- Отделен из общего манифеста hipster-shop еще один микросервис и кастомизировал его.

Задания со * не выполнены
После выполнения задания кластер был потушен

## Kubernetes-Operators

- Создал cr и crd согласно документации в интернете для новой apiVersion
- Написал свой operator согласно инструкции

```
export MYSQLPOD=$(kubectl get pods -l app=mysql-instance -o jsonpath="{.items[*].metadata.name}")
kubectl exec -it $MYSQLPOD -- mysql -potuspassword -e "select * from test;" otus-database
+----+-------------+
| id | name |
+----+-------------+
| 1 | some data |
| 2 | some data-2 |
| 3 | some data-3 |
| 4 | some data-4 |
+----+-------------+

kubectl get jobs
NAME COMPLETIONS DURATION AGE
restore-mysql-instance-job 1/1 10s 8m44s
```


## Kubernetes-Monitoring

- Создан кластер kind
- Создан костомный контейнер nginx
- Написан деплоймент с контейнером nginx-exporter
- Написан сервис
- Написан сервисмонитор согласно интрукции

## Kubernetes-Logging

Развернут кластер в яндекс облаке
otus@linux:~$ kubectl get nodes

```
NAME STATUS ROLES AGE VERSION
cl1i8i4254toic9otp36-ixuz Ready 3m10s v1.20.11
cl1psh2gs2jl8gst29di-oxyk Ready 2m47s v1.20.11
cl1psh2gs2jl8gst29di-upaf Ready 2m53s v1.20.11
cl1psh2gs2jl8gst29di-uvam Ready 2m50s v1.20.11
```

Установлены микросервисы.

```
otus@linux:~$ kubectl get pods -n microservices-demo -o wide
NAME READY STATUS RESTARTS AGE IP NODE NOMINATED NODE READINESS GATES
adservice-56d56d89cc-t9wcc 0/1 ContainerCreating 0 50s cl1i8i4254toic9otp36-ixuz
cartservice-c8b9fc586-l4pr8 0/1 ContainerCreating 0 51s cl1i8i4254toic9otp36-ixuz
checkoutservice-74f4c5464f-9cxtt 1/1 Running 0 52s 10.112.128.9 cl1i8i4254toic9otp36-ixuz
currencyservice-7df4d74b7c-rqjfj 0/1 ContainerCreating 0 50s cl1i8i4254toic9otp36-ixuz
emailservice-86794489df-b7pqb 1/1 Running 0 53s 10.112.128.8 cl1i8i4254toic9otp36-ixuz
frontend-cf49f7975-x56cj 0/1 ContainerCreating 0 52s cl1i8i4254toic9otp36-ixuz
loadgenerator-7fdb874b-r6vh5 0/1 ContainerCreating 0 50s cl1i8i4254toic9otp36-ixuz
paymentservice-5768d9bb67-p2k5c 0/1 ContainerCreating 0 51s cl1i8i4254toic9otp36-ixuz
productcatalogservice-84fd74ccc9-9xgq6 0/1 ContainerCreating 0 51s cl1i8i4254toic9otp36-ixuz
recommendationservice-6fcb597467-cbbwp 0/1 ContainerCreating 0 52s cl1i8i4254toic9otp36-ixuz
redis-cart-55d76945cb-bwktg 0/1 ContainerCreating 0 50s cl1i8i4254toic9otp36-ixuz
shippingservice-6bc75ffff-lcj7s 0/1 ContainerCreating 0 50s cl1i8i4254toic9otp36-ixuz
```

Установлены средством helm
- elasticsearch
- kibana
- fluent-bit

Установлен prometheus-operator в неймспейс observability

Установилен loki

```
helm repo add loki https://grafana.github.io/loki/charts
helm repo update
helm upgrade --install loki loki/loki-stack --namespace observability -f loki.values.yaml
```

## Kubernetes-Gitops

Развернут кластер в yc
Создан репозиторий в https://gitlab.com/Xyrma/microservices-demo/
Скпированы туда готовые чарты из https://gitlab.com/express42/kubernetes-platform-demo/microservices-demo/
Создан .gitlab-ci.yaml
Собраны из запушены образы для каждого микросервиса в докерхаб
Установлен в кластер helmrelease
```
kubectl apply -f https://raw.githubusercontent.com/fluxcd/helmoperator/master/deploy/flux-helm-release-crd.yaml
```
добавлен репо
```
helm repo add fluxcd https://charts.fluxcd.io/
```
Установлен flux
Установлен helm операртор
установлен fluxctl на лоакальную машину

```
kubectl get helmrelease -n microservices-demo
NAME RELEASE PHASE STATUS MESSAGE AGE
frontend frontend Succeeded deployed Release was successful for Helm release 'frontend' in 'microservices-demo'. 46m
```

Установлен flagger
```
helm repo add flagger https://flagger.app/
kubectl apply -f https://raw.githubusercontent.com/weaveworks/flagger/master/artifacts/flagger/crd.yaml
helm upgrade --install flagger flagger/flagger
```