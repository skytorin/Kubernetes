# Kubernetes

## Установка kubectl в Linux
1. Загружаем последнюю версию kubectl с помощью команды:
```
curl -LO https://storage.googleapis.com/kubernetes-release/release/`curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt`/bin/linux/amd64/kubectl
```
или определенную версию
```
curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.19.0/bin/linux/amd64/kubectl
```

2. Делаем двоичный файл kubectl исполняемым:
```
chmod +x ./kubectl
```

3. Перемещаем двоичный файл в директорию из переменной окружения PATH:
```
sudo mv ./kubectl /usr/local/bin/kubectl
```

4. Проверяем версию :
```
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

Псевдоним для kubectl, который можно интегрировать с автодополнениями
```bash
alias k=kubectl
complete -F __start_kubectl k
```

## Быстрое переключение контекста и namespace
Установка kubeens и kubectx
```
git clone https://github.com/ahmetb/kubectx
sudo cp kubectx /usr/local/bin/
sudo cp kubens /usr/local/bin/
```

Перечислить все контексты
```
kubectx
```

Переключиться на указанный контекст
```
kubectx kubernetes-admin@kubernetes
```

Перечислить все пространства имен
```
kubens
```

Переключиться в назначенное пространство имен
```
kubens kube-system
```









