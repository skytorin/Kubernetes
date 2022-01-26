# Kubernetes
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
