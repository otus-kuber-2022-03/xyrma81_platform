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
