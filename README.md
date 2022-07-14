# Kubernetes (k8s)

## Использование Minikube
Веб дашборд с информацией о класере
```bash
minikube dashboard
```
Создание сервиса в minikube
```bash
minikube service app-deployment
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

4. Проверяем версию :
```bash
kubectl version --client
```


## Автодополнение ввода для Kubectl в BASH
Настройка автодополнения в текущую сессию bash, предварительно должен быть установлен пакет bash-completion
```bash
source <(kubectl completion bash) 
```

Добавление автодополнения autocomplete постоянно в командную оболочку bash
```bash
echo "source <(kubectl completion bash)" >> ~/.bashrc 
```

Псевдоним для kubectl, который можно интегрировать с автодополнениями:
```bash
alias k=kubectl
complete -F __start_kubectl k
```


## Быстрое переключение контекста и namespace
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
kubectx kubernetes-admin@kubernetes
```

Перечислить все пространства имен:
```bash
kubens
```

Переключиться в назначенное пространство имен:
```bash
kubens kube-system
```









