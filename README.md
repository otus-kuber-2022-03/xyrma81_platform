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

## Kubernetes-Vault 


### helm status vault

```
xyrma@xyrma:~$ helm status vault
NAME: vault
LAST DEPLOYED: Mon Aug  1 11:48:19 2022
NAMESPACE: default
STATUS: deployed
REVISION: 1
NOTES:
Thank you for installing HashiCorp Vault!

Now that you have deployed Vault, you should look over the docs on using
Vault with Kubernetes available here:

https://www.vaultproject.io/docs/


Your release is named vault. To learn more about the release, try:

  $ helm status vault
  $ helm get manifest vault
```

### kubectl exec -it vault-0 -- vault operator init --key-shares=1 --key-threshold=1

```
xyrma@xyrma:~$ kubectl exec -it vault-0 -- vault operator init --key-shares=1 --key-threshold=1
Unseal Key 1: 2rNygKqWucIzVtpAf5UUGfPs0yvLNEzSd00DXpxQVLk=

Initial Root Token: hvs.LNhQ0eyeaj34ldPKMpINJQZu

Vault initialized with 1 key shares and a key threshold of 1. Please securely
distribute the key shares printed above. When the Vault is re-sealed,
restarted, or stopped, you must supply at least 1 of these keys to unseal it
before it can start servicing requests.

Vault does not store the generated root key. Without at least 1 keys to
reconstruct the root key, Vault will remain permanently sealed!

It is possible to generate new unseal keys, provided you have a quorum of
existing unseal keys shares. See "vault operator rekey" for more information.

```

### kubectl exec -it vault-0 -- vault login

```
xyrma@xyrma:~$ kubectl exec -it vault-0 -- vault login
Token (will be hidden): 
Success! You are now authenticated. The token information displayed below
is already stored in the token helper. You do NOT need to run "vault login"
again. Future Vault requests will automatically use this token.

Key                  Value
---                  -----
token                hvs.LNhQ0eyeaj34ldPKMpINJQZu
token_accessor       qWFFZQp0rET5ZnhcI89q6JDf
token_duration       ∞
token_renewable      false
token_policies       ["root"]
identity_policies    []
policies             ["root"]

```

### Вывод команды чтения секрета

```
xyrma@xyrma:~$ kubectl exec -it vault-0 -- vault read otus/otus-ro/config
Key                 Value
---                 -----
refresh_interval    768h
password            asajkjkahs
username            otus
zeph1rr@Zeph1rr-pc:~$ kubectl exec -it vault-0 -- vault kv get otus/otus-rw/config
====== Data ======
Key         Value
---         -----
password    asajkjkahs
username    otus

```

### Обновленный список авторизаций

```
xyrma@xyrma:~$ kubectl exec -it vault-0 -- vault auth list
Path           Type          Accessor                    Description
----           ----          --------                    -----------
kubernetes/    kubernetes    auth_kubernetes_64979251    n/a
token/         token         auth_token_b980a206         token based credentials
```

### Работа с контейнерами vault-agent

Итоговый файл [index.html](kubernetes-vault/index.html)
Конфиг инит контейнера в kubernetes-vault/example-k8s-spec.yaml переделан для работы по https.
- Использование vault в качестве CA.
```bash
kubectl exec -it vault-0 -- vault write pki_int/issue/example-dot-ru common_name="gitlab.example.ru" ttl="24h"
Key                 Value
---                 -----
ca_chain            [-----BEGIN CERTIFICATE-----
MIIDnDCCAoSgAwIBAgIUJQeRmEvg38wV7HyhHXHaSKXGfwwwDQYJKoZIhvcNAQEL
BQAwFTETMBEGA1UEAxMKZXhtYXBsZS5ydTAeFw0yMDA2MTYwNzM0MDhaFw0yNTA2
MTUwNzM0MzhaMCwxKjAoBgNVBAMTIWV4YW1wbGUucnUgSW50ZXJtZWRpYXRlIEF1
dGhvcml0eTCCASIwDQYJKoZIhvcNAQEBBQADggEPADCCAQoCggEBAMac7l3dm6uQ
0bgHySOU6EiE1l6YtqSBFPDVpmnJDyNnMn8n/tZH9AISit0B+4wM6gagfchEzbii
ZS99h9wqYk55piNkfkO8yUOgxUw9yTcWaC2bdnZZ4OZHgPPtd8tgGalcV7MDgyTi
n+pP0KL2roWKzbEuybnbZ3XYuXo+lsAd4a2JYtTI/3a04aaPuIBx/TIDHwlb56Wy
6BDUblvcyplDod/0B/mRbxqyh0be1WRuUnHggMccMfNUEF73hrxxof7IpHaGQVHc
oMR1IOdQxR9EpJPdOdNtCidSzBLH/CijQylDck5iImh5oKVL4Pu6gRtrNfJmEw4v
AdLn4nt1yxUCAwEAAaOBzDCByTAOBgNVHQ8BAf8EBAMCAQYwDwYDVR0TAQH/BAUw
AwEB/zAdBgNVHQ4EFgQUVt66P7FzKF96sTpZUAlT0cUhCXcwHwYDVR0jBBgwFoAU
jlgrHlD+qyErlnUGNj0NXDGZ/4gwNwYIKwYBBQUHAQEEKzApMCcGCCsGAQUFBzAC
hhtodHRwOi8vdmF1bHQ6ODIwMC92MS9wa2kvY2EwLQYDVR0fBCYwJDAioCCgHoYc
aHR0cDovL3ZhdWx0OjgyMDAvdjEvcGtpL2NybDANBgkqhkiG9w0BAQsFAAOCAQEA
EUakzY/EiLtj5jGqCPE5/0TCXbPssbhXWo97f2oizkQpaI7b8Fc/Rw7h3NdDMF5h
T2JXnEez+j8DttLNtBLgvA0yveMeDRyKk8sJLSG8vKOie4d0awGRDrJ4IZ65WjtK
lN21jIylizvN4K6HPq9ZwZlpzjotB9ex+bs2Ye5uTfVens8VW/GWF8xXxhpDJG+x
10IedMk8KRpbSIwNvinZpe/cirtA/emwIGrac4JH9JI+q3wB4iIsKKGKfJRhHFUa
zARc6uXCeAGbn+oontMASi+zsGWKIIJ07SUQxoK45q1eSlbrooCDiUiLUlENXdyP
1DaklS1sPKg/R6UrRK9TyA==
-----END CERTIFICATE-----]
certificate         -----BEGIN CERTIFICATE-----
MIIDZzCCAk+gAwIBAgIUex8RqbWqW2fIXbA38ptJB9nA26cwDQYJKoZIhvcNAQEL
BQAwLDEqMCgGA1UEAxMhZXhhbXBsZS5ydSBJbnRlcm1lZGlhdGUgQXV0aG9yaXR5
MB4XDTIwMDYxNjA3Mzk1OFoXDTIwMDYxNzA3NDAyN1owHDEaMBgGA1UEAxMRZ2l0
bGFiLmV4YW1wbGUucnUwggEiMA0GCSqGSIb3DQEBAQUAA4IBDwAwggEKAoIBAQC4
nJN4PHZBPuY24FgQfoVU9+r6iJofhde4nCtbH0cg8w77bgw18T7eQh6Cz0/fYGnK
S2cVcxiWTn3edEw32qVFMBezfPO5cLKqYqYGUs07r70r7ec7Jv9TsVKRXNmL7uDL
vN3cme+BmV7y6FAuafU5m3XdN8KXtyAiDe70jr6Mim7eXKaxx+qzPYGQL4yG3Ad5
ATtlwelxIqw++PJLEt6vbWayUFdFK0pHp7fE/t+7Xjr6kslf0j038EgDyYgSCD2l
3WG6JV7Nb/jJMJmSEOJy4Ln5W69n3uPyjvaz3ssDCp7qZQBSQH5YUbzJUozdrjwY
jiiDeUCeAsXujfQ3GZZ/AgMBAAGjgZAwgY0wDgYDVR0PAQH/BAQDAgOoMB0GA1Ud
JQQWMBQGCCsGAQUFBwMBBggrBgEFBQcDAjAdBgNVHQ4EFgQUuPKWEsDgBgL+tj+f
9ZdiwlDT554wHwYDVR0jBBgwFoAUVt66P7FzKF96sTpZUAlT0cUhCXcwHAYDVR0R
BBUwE4IRZ2l0bGFiLmV4YW1wbGUucnUwDQYJKoZIhvcNAQELBQADggEBAJwMLvYo
fRhUEEZyNQtvuDp4L84N1qlj4YVRWYigBceWosTm8H2QWzlLsV+4Yl5UsZltPObK
2T8gM6t27ujI9FyyTeNGbqAmaJ31E6SyL1uYr+mlAVFA7eKEPzq6EpGfwqWy7MlI
xcASmV4OJC5TJhDaZ3XUiJ/IgT9E2kPmrw03NnTzK9qG6wAiU1HnSMdaqY1FTxoO
NdTHpIqID4HedCMWcsoVwcVEzPinOle3L75wq1G6to3N/KScAx+QUOTCSJwKjxD9
GSV4aXoaebJ3TJrz6zudL7pMD6vTcxy3BNT1Jg4/+xF7XCv/9xwN86+E9aYoiWK+
fsNHpQNk0FY7s9E=
-----END CERTIFICATE-----
expiration          1592379627
issuing_ca          -----BEGIN CERTIFICATE-----
MIIDnDCCAoSgAwIBAgIUJQeRmEvg38wV7HyhHXHaSKXGfwwwDQYJKoZIhvcNAQEL
BQAwFTETMBEGA1UEAxMKZXhtYXBsZS5ydTAeFw0yMDA2MTYwNzM0MDhaFw0yNTA2
MTUwNzM0MzhaMCwxKjAoBgNVBAMTIWV4YW1wbGUucnUgSW50ZXJtZWRpYXRlIEF1
dGhvcml0eTCCASIwDQYJKoZIhvcNAQEBBQADggEPADCCAQoCggEBAMac7l3dm6uQ
0bgHySOU6EiE1l6YtqSBFPDVpmnJDyNnMn8n/tZH9AISit0B+4wM6gagfchEzbii
ZS99h9wqYk55piNkfkO8yUOgxUw9yTcWaC2bdnZZ4OZHgPPtd8tgGalcV7MDgyTi
n+pP0KL2roWKzbEuybnbZ3XYuXo+lsAd4a2JYtTI/3a04aaPuIBx/TIDHwlb56Wy
6BDUblvcyplDod/0B/mRbxqyh0be1WRuUnHggMccMfNUEF73hrxxof7IpHaGQVHc
oMR1IOdQxR9EpJPdOdNtCidSzBLH/CijQylDck5iImh5oKVL4Pu6gRtrNfJmEw4v
AdLn4nt1yxUCAwEAAaOBzDCByTAOBgNVHQ8BAf8EBAMCAQYwDwYDVR0TAQH/BAUw
AwEB/zAdBgNVHQ4EFgQUVt66P7FzKF96sTpZUAlT0cUhCXcwHwYDVR0jBBgwFoAU
jlgrHlD+qyErlnUGNj0NXDGZ/4gwNwYIKwYBBQUHAQEEKzApMCcGCCsGAQUFBzAC
hhtodHRwOi8vdmF1bHQ6ODIwMC92MS9wa2kvY2EwLQYDVR0fBCYwJDAioCCgHoYc
aHR0cDovL3ZhdWx0OjgyMDAvdjEvcGtpL2NybDANBgkqhkiG9w0BAQsFAAOCAQEA
EUakzY/EiLtj5jGqCPE5/0TCXbPssbhXWo97f2oizkQpaI7b8Fc/Rw7h3NdDMF5h
T2JXnEez+j8DttLNtBLgvA0yveMeDRyKk8sJLSG8vKOie4d0awGRDrJ4IZ65WjtK
lN21jIylizvN4K6HPq9ZwZlpzjotB9ex+bs2Ye5uTfVens8VW/GWF8xXxhpDJG+x
10IedMk8KRpbSIwNvinZpe/cirtA/emwIGrac4JH9JI+q3wB4iIsKKGKfJRhHFUa
zARc6uXCeAGbn+oontMASi+zsGWKIIJ07SUQxoK45q1eSlbrooCDiUiLUlENXdyP
1DaklS1sPKg/R6UrRK9TyA==
-----END CERTIFICATE-----
private_key         -----BEGIN RSA PRIVATE KEY-----
MIIEowIBAAKCAQEAuJyTeDx2QT7mNuBYEH6FVPfq+oiaH4XXuJwrWx9HIPMO+24M
NfE+3kIegs9P32BpyktnFXMYlk593nRMN9qlRTAXs3zzuXCyqmKmBlLNO6+9K+3n
Oyb/U7FSkVzZi+7gy7zd3JnvgZle8uhQLmn1OZt13TfCl7cgIg3u9I6+jIpu3lym
scfqsz2BkC+MhtwHeQE7ZcHpcSKsPvjySxLer21mslBXRStKR6e3xP7fu146+pLJ
X9I9N/BIA8mIEgg9pd1huiVezW/4yTCZkhDicuC5+VuvZ97j8o72s97LAwqe6mUA
UkB+WFG8yVKM3a48GI4og3lAngLF7o30NxmWfwIDAQABAoIBADCOFgdYt62fcoNa
bC8iZ8UaU7ZDOW4zELLgeFLGHjofU4BzyEhjxCpG76luB070F776KAmvNPdLe7WH
lwhVvIQ/CuzNX3kVmBhSS+J74rjhFvs33kpjjmIf0FylNB6m3H8ZlKzR2/mVMjDn
QzeB7NqS9eQSJ18p7gym54NxC9MAn5dz3p0GSe8pWq4hXy7/xRU3T5GjLwUSU+T3
DZP8+7l/FEvgMsV6G0deQVam9iQr7cR6HQ8OOUNMjUaM7w+GUNV4iLUii3JDSQd7
R1QnrEwFi+VyEANli/JOdLmn03knN/MAg+DOJK70w6SgaKMcbW/nH/u0sG3aq6jB
j5F1hNkCgYEA1Hv+XxoWaVPb3XoNRCungJfrU3IFta7s52tFOV0UxRqsxfXFnwOx
NrKaRQlzFUco0RqgjF7pLxbXYJDJ1+gNoWc3K6vZWeSyqWWiBxtn9eqrChxgPSE/
ZN9LwheH4nxi5nsh0EvcqfdPSXdYzI5SbRDyhEWFauvBVsyCll2N6i0CgYEA3mtJ
j3oJLQ1pAoG/xCPpqGotKsksdPvcBSVImnQFgBiBZGEqmrSf3O997Mz6QuopDsw1
wueVesMiA7m4RZDlaVnSkhyvQAWlIIj2xmTLC+7pe9ZrGF8LvvCm49/zkBlOXuPX
izH6xphTZgl0IDrY7T+ICfbcpi1rfJjikGAOitsCgYAKUD5nhU+jKyPX2y27qlbG
Ahm1AirOx7/N98HzZ9YzPvk13pkJ/9bhLcgZI71HQh30EFPMnGq7E2O+1yhE54mJ
1QWzg/LXzybw2/MCX00rfYlxwzDUpsF59vCpahT5ZEo0n7NjddsvEMbzbOyNeTb8
/j6XNvyj1O+cc+6+t6nEvQKBgCrX38OTblEPVDr3Y0kU4d1fFnQ3bCjcmvUiyWl3
D9gs4D/Ft781K9YTC96hXVOmZ2JCU9jHYzPSgqrVC3na/1Xbx4P9ooRikfxCZcax
g6s4yiDgnKCFLm4JTRx39yK6vS3qFYrqhbPbg7UT/Rp4O3D32+yPcNFRznKhwIKu
/h4hAoGBAJJr7C+DA81dsmpnSmLPbzrQE1Gc/5woO+LVZoeIe7e70iQCMv2muno7
9LPomPfR+WakYEP6JSj0d+38Laj6UNH3yh6dVi0hCJlTVy6Vn3Rg246xvQW8Jm5+
eOqgnSmTzYSud1a0yuOg+wWYjps6XIxqXTQaApI5YjXxbg2Dm0C9
-----END RSA PRIVATE KEY-----
private_key_type    rsa
serial_number       7b:1f:11:a9:b5:aa:5b:67:c8:5d:b0:37:f2:9b:49:07:d9:c0:db:a7
```

## Kubernetes-Storege

- Подготовлен файл cluster.yaml с необходимой конфигурацией для kind;
- В директории hw созданы манифесты для создания объектов StorageClass, pvc и pod;
- Задание со * - развернут iscsi (добавлен диск lvm), в под добавлен volume iscsi.

## Kubernetes-Production-Clusters

# Подготовка

развернут 1 `master` и 3 `worker`

На всех нодах выполнена установка необходимых пакетов

---

# Создание кластера

на мастере
```
kubeadm init --pod-network-cidr=192.168.0.0/24
```

```
  mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config
```
```
root@master-0:~# kubectl get nodes
NAME       STATUS     ROLES    AGE     VERSION
master-0   NotReady   master   4m10s   v1.17.4
```
устанавливаем calico
```
kubectl apply -f https://docs.projectcalico.org/manifests/calico.yaml
```

добавляем ноды
```
kubeadm join 10.132.0.43:6443 --token 3yfonj.jke7kufzxgzogefa --discovery-token-ca-cert-hash sha256:fc63458bc01476316a192e965be4f748306bc66dd97a5585accca82df9ab7c36
```

```
root@master-0:~# kubectl get nodes
NAME       STATUS   ROLES    AGE     VERSION
master-0   Ready    master   8m37s   v1.17.4
worker-0   Ready    <none>   42s     v1.17.4
worker-1   Ready    <none>   41s     v1.17.4
worker-2   Ready    <none>   42s     v1.17.4
```
```
kubectl apply -f deployment.yaml
```
```
kubectl get po -o wide
NAME                               READY   STATUS    RESTARTS   AGE   IP              NODE       NOMINATED NODE   READINESS GATES
nginx-deployment-c8fd555cc-6lzjg   1/1     Running   0          37s   192.168.0.193   worker-2   <none>           <none>
nginx-deployment-c8fd555cc-wqcg8   1/1     Running   0          37s   192.168.0.130   worker-0   <none>           <none>
nginx-deployment-c8fd555cc-x7m9c   1/1     Running   0          37s   192.168.0.129   worker-0   <none>           <none>
nginx-deployment-c8fd555cc-zw4s8   1/1     Running   0          37s   192.168.0.1     worker-1   <none>           <none>
```

---

# Обновление

на мастере
```
apt-get update && apt-get install -y kubeadm=1.18.0-00 \
kubelet=1.18.0-00 kubectl=1.18.0-00
```
```
root@master-0:~# kubectl get nodes
NAME       STATUS   ROLES    AGE   VERSION
master-0   Ready    master   19m   v1.18.0
worker-0   Ready    <none>   11m   v1.17.4
worker-1   Ready    <none>   11m   v1.17.4
worker-2   Ready    <none>   11m   v1.17.4
```

обновление
```
kubeadm upgrade plan
kubeadm upgrade apply v1.18.0
```


выводим ноды из кластера
```
kubectl drain worker-0 --ignore-daemonsets
kubectl drain worker-1 --ignore-daemonsets
kubectl drain worker-2 --ignore-daemonsets
```

на worker нодах выполняем
```
apt-get install -y kubelet=1.18.0-00 kubeadm=1.18.0-00
systemctl restart kubelet
kubectl uncordon worker-0
kubectl uncordon worker-1
kubectl uncordon worker-2
```

```
root@master-0:~# kubectl get nodes
NAME       STATUS   ROLES    AGE   VERSION
master-0   Ready    master   42m   v1.18.0
worker-0   Ready    <none>   34m   v1.18.0
worker-1   Ready    <none>   34m   v1.18.0
worker-2   Ready    <none>   34m   v1.18.0
```

---

# Kubespray

```
git clone https://github.com/kubernetes-sigs/kubespray.git
cd kubespray/
sudo pip install -r requirements.txt
cp -rfp inventory/sample inventory/mycluster
```
отредактирован [inventory.ini](inventory.ini)

установка кластера
```
ansible-playbook -i inventory/mycluster/inventory.ini --become --become-user=root \
--user=${SSH_USERNAME} --key-file=${SSH_PRIVATE_KEY} cluster.yml
```

```
root@node1:~# kubectl get nodes
NAME    STATUS   ROLES    AGE     VERSION
node1   Ready    master   6m10s   v1.19.2
node2   Ready    <none>   4m56s   v1.19.2
node3   Ready    <none>   4m56s   v1.19.2
node4   Ready    <none>   4m56s   v1.19.2
```
---

## Kubernetes-Debug

### Выполнено
- Ознакомились с работой `kubectl debug`, выявили проблему с агентом debug;
- Установили kube-iptables-tailer и необходимые для него сервис аккаунт, роль и биндинг;
- Установили тестовое приложение netperf-operator (оператор, который позволяет запускать тесты
пропускной способности сети между нодами кластера); 
- Добавили сетевую потилику Calico для эмуляции сетевой проблемы;
- Посмотрели логи calico на воркер-ноде `journalctl -k | grep calico-pack`;
- Запустили iptables-tailer для диагностики сетевой проблемы и добились того, чтобы iptables-tailer нормально запустился и писал лог;

### Выполнено задание со *
- Исправлена ошибка в сетевой политике, чтобы netperf заработал; 
- Исправлен манифест DaemonSet, чтобы показывались имена подов место ip адресов(?). 

### Как запустить: 
#### Предварительные действия: 
- Развернуть кластер (kind не подходит, нужен полноценный кластер минимум с 2 воркер нодами (минимум 2 ноды нужно для работы тестового приложения netperf-operator)); 
- Установить kubectl debug, согласно документации https://github.com/aylei/kubectl-debug
- Клонировать репозиторий netperf-operator - `git clone https://github.com/piontec/netperf-operator.git`
- Выполнить манифесты для запуска оператора в кластере: 
```
cd kubernetes-debug/netperf-operator
kubectl apply -f ./deploy/crd.yaml
kubectl apply -f ./deploy/rbac.yaml
kubectl apply -f ./deploy/operator.yaml

```

#### Основные действия: 
##### Задание 1 (проблема с контейнером-агентом):
При выполнении strace получаем ошибку вида: 

```
bash-5.0# strace -c -p1
strace: test_ptrace_get_syscall_info: PTRACE_TRACEME: Operation not permitted
strace: attach: ptrace(PTRACE_ATTACH, 1): Operation not permitted
```

Смотрим на наличие capabilities с использованием команды `docker inspect` (выполняем для запущенного debug контейнера на воркер-ноде):

```
            "CapAdd": null,
            "CapDrop": null,
``` 

Смотри добавляются ли необходимые capabilities в коде (по той ссылке что в подсказке): 
```
CapAdd:      strslice.StrSlice([]string{"SYS_PTRACE", "SYS_ADMIN"}),
```
- в коде все в порядке.

Смотрим версию образа агента: 

```
Normal  Pulling    16m   kubelet, node2     Pulling image "aylei/debug-agent:0.0.1"
```
- версия подозрительно старая. 

Смотри код в старой версии по ссылке https://github.com/aylei/kubectl-debug/blob/0.0.1/pkg/agent/runtime.go - а нужной строчки с capabilities там нет. 

Удаляем агента: 
`kubectl delete -f https://raw.githubusercontent.com/aylei/kubectl-debug/master/scripts/agent_daemonset.yml`

Устанавливаем последнюю версию агента, используя такой же манифест как и официальный, только с измененной версий образа (изменена на latest):
`kubectl apply -f kubernetes-debug/strace/01-agent_daemonset.yaml`

После этого еще раз проверяем strace и видим, что все успешно отрабатывает:

```
bash-5.0# strace -c -p1
strace: Process 1 attached
^Cstrace: Process 1 detached
% time     seconds  usecs/call     calls    errors syscall
------ ----------- ----------- --------- --------- ----------------
  0.00    0.000000           0         2           poll
  0.00    0.000000           0         1           restart_syscall
------ ----------- ----------- --------- --------- ----------------
100.00    0.000000                     3           total
```

##### Задание 2 (диагностика сетевой проблемы):
Выполнить уже исправленные манифесты в следующей последовательности: 
- `kubectl apply -f kit/kit-clusterrole.yaml`;
- `kubectl apply -f kit/kit-serviceaccount.yaml`;
- `kubectl apply -f kit/kit-clusterrolebinding.yaml`;
- `kubectl apply -f kit/netperf-calico-policy.yaml`;
- `kubectl apply -f kit/iptables-tailer.yaml`;

Для запуска тестового приложения выполнить: 
- `kubectl apply -f netperf-operator/deploy/cr.yaml`;


##### Задание со `*`:
- Для исправления ошибки в сетевой политике необходимо исправить и применить манифест `kit/netperf-calico-policy.yaml`. Нужно строчки `selector: netperf-role == "netperf-client"` заменить на `selector: netperf-type in {"client", "server"}` (согласно документации https://docs.projectcalico.org/v3.7/reference/calicoctl/resources/globalnetworkpolicy#selector). И после этого запустить для проверки тест еще раз;
-  Возможно, судя по документации (https://github.com/box/kube-iptables-tailer), для того, чтобы отображалось имя пода, необходимо в DaemonSet изменить значение переменной окружения POD_IDENTIFIER с `label` на `name` (файл `kit/iptables-tailer.yaml`) и применить манифест, но я разницы не заметил. У меня в обоих случаях в поле `OBJECT` отображается имя пода, а в `MESSAGE` присутствует его ip адрес, делалось все на кластере GCE v1.14.  