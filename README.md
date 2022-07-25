# Kubernetes (k8s)

## Minikube
Установка Minikube:
```bash
curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 \
&& chmod +x minikube
```

Чтобы исполняемый файл Minikube был доступен из любой директории, выполняем следующие команды:
```bash
sudo mkdir -p /usr/local/bin/
sudo install minikube /usr/local/bin/

```
Запуск Minikube в Docker:
```bash
minikube start --vm-driver=none
```

Статус Minikube:
```bash
minikube status
```

Очистка локального состояния (при ошибках запуска Minikube):
```bash
minikube delete
```

Веб-дашборд с информацией о класере:
```bash
minikube dashboard
```

Создание сервиса в minikube:
```bash
minikube service {name_deployment}
```


## Установка kubectl в Linux
1. Загружаем последнюю версию kubectl с помощью команды:
```bash
curl -LO https://storage.googleapis.com/kubernetes-release/release/`curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt`/bin/linux/amd64/kubectl
```
или определенную версию:
```bash
export KUBECTL_VERSION=v1.19.2
curl -LO "https://storage.googleapis.com/kubernetes-release/release/${KUBECTL_VERSION}/bin/linux/amd64/kubectl"
```
2. Перемещаем двоичный файл в директорию из переменной окружения PATH:
```bash
sudo mv kubectl /usr/local/bin/kubectl
```

3. Делаем двоичный файл kubectl исполняемым:
```bash
sudo chmod +x /usr/local/bin/kubectl
````

4. Проверяем версию:
```bash
kubectl version --client
```


## Автодополнение ввода для Kubectl в BASH
Настройка автодополнения в текущую сессию bash, предварительно должен быть установлен пакет bash-completion:
```bash
source <(kubectl completion bash) 
```

Добавление автодополнения autocomplete постоянно в командную оболочку bash:
```bash
echo "source <(kubectl completion bash)" >> ~/.bashrc 
```

Псевдоним для kubectl, который можно интегрировать с автодополнениями:
```bash
alias k=kubectl
complete -F __start_kubectl k
```


## Контексты и пространства имен 
### Внешние утилиты для быстрого переключения
Установка kubens и kubectx:
```bash
git clone https://github.com/ahmetb/kubectx
sudo cp kubectx /usr/local/bin/
sudo cp kubens /usr/local/bin/
```

Перечислить все контексты:
```bash
kubectx
```

Переключиться на указанный контекст:
```bash
kubectx {name_context}
```

Перечислить все пространства имен:
```bash
kubens
```

Переключиться в назначенное пространство имен:
```bash
kubens {name_space}
```

### Команды для работы контекстами и пространствами имен
Показать все доступные контексты:
```bash
kubectl config get-contexts
```

Показать текущий контекст:
```bash
kubectl config current-context 
```

Установить указанный контекст как текущий:
```bash
kubectl config use-context my_context
```

Изменить namespace для всех последующих команд kubectl в текущем контексте:
```bash
kubectl config set-context --current --namespace={namespace}
```


## Перезапуск PODов

Вариант 1
```bash
kubectl scale deployment --replicas=0 {name_deployment}
kubectl scale deployment --replicas=3 {name_deployment}
```

Вариант 2
```bash
kubectl rollout restart deployment {name_deployment}
```


## Логи PODов

Сохранение последних 50 строк лога в файл
```bash
kubectl.exe logs {name_pod} --namespace {name_space} --tail=50 > {name_pod}.log
```

Сохранение логов в файл за последний промежуток времени:
```bash
# последние двадцать минут
kubectl.exe logs {name_pod} --namespace {name_space} --since=20m > {name_pod}.log  
# последние три часа
kubectl.exe logs {name_pod} --namespace {name_space} --since=3h > {name_pod}.log  
# последние два дня
kubectl.exe logs {name_pod} --namespace {name_space} --since=2d > {name_pod}.log  
```

Сохранение логов в файл c указанного времени:
```bash
kubectl.exe logs {name_pod} --namespace {name_space} --since-time=2022-05-13T15:00:00Z > {name_pod}.log  
```

## Разное

Показать версию приложения
```bash
kubectl get pods -n {name_space} -o jsonpath="{.items[*].spec.containers[*].image}" | tr -s '[[:space:]]' '\n'
```

Зайти в консоль пода/контейнера:
```bash
kubectl exec -i -t -n {name_space} {name_pod} -c {name_container} -- sh -c "clear;  (bash || ash || sh)"
```

Форвард порта пода на локальный порт хоста
```bash
kubectl.exe port-forward svc/rabbitmq 33333:15672 -n {name_space}
```

Получить yaml настроек пода (сервиса, репликасета, деплоймента и т.д.):
```bash
kubectl get -n {name_space} {name_pod} -o yaml
```













