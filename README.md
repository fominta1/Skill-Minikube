Разверните аналогичное веб-приложение на кластере 
# Minikube


В качестве образов для двух контейнеров можно (но не обязательно) использовать уже созданные нами в модулях по Docker образы.
Единственное отличие от приведённого примера — наши образы не представлены в публичном репозитории, поэтому их нужно вручную загрузить внутрь кластера:
minikube cache add <название локального образа>
Кроме того, файл index.php нужно чуть переписать, т. к. у нас адрес до БД и логин/пароль прописаны статически в самом файле.
А должны браться из переменных окружения.
Если используете публичные образы, проследите, чтобы образ веб-приложения брал данные для подключения к БД из переменных окружения.
Использовать уже приведённые образы запрещено.

Помимо этого, необходимо сделать таблицу (например, в формате Excel) с инвентаризацией вашего кластера. В кратком виде указать установленное ПО на нодах, количество нод, ОС на нодах, адреса.

Условия реализации
В качестве ответа предоставьте:

## все конфигурационные файлы,
## скриншот из браузера с работающим веб-приложением,
## вывод команды kubectl get all -o wide,
## табличку с инвентаризацией.

![](table.xlxs)

Результаты работы загрузите на свой GitHub. В качестве ответа приложите ссылку на репозиторий.

# Commands to run

```bash
# delete if exists
minikube delete -p tanya-k8s

# create
minikube config set driver virtualbox
minikube kubectl -- get po -A
minikube start --nodes 3 -p tanya-k8s --driver=virtualbox

# deploynment
minikube config set profile tanya-k8s
alias kubectl="minikube kubectl --"
kubectl apply -f 1_configmap.yaml,2_mongo-secret.yaml,3_database.yaml,4_webapp.yaml

# addons for dashboard
minikube -p tanya-k8s addons enable metrics-server

# dashboard
minikube dashboard -p tanya-k8s &!

# exposing service
minikube service webapp-service
```
