# Добавляем конфиг CI/CD в Gitlab

В этой части добавляем последний шаг - конфиг для Gitlab CI/CD для сборки, тестирования и деплоя приложения в кластер k8s. Деплой производится с использованием утилиты Helm v3.

Gitlab CI/CD описывается в файле `.gitlab-ci.yml` в формате `yaml`. По умолчанию Gitlab ищет этот файл в корне проекта, путь до файла может быть переопределен в настройках проекта.

## 1. Подготавливаем CI/CD

Для этого скопируем заранее подготовленный шаблон `.gitlab-ci.yml` в проект `xpaste`, выполнив команду:

```bash
cp .gitlab-ci.yml ~/xpaste/
```

## 2. Адрес Kubernetes API

В файле `.gitlab-ci.yml` указан адрес kube api. Так как runner запущен внутри кластера кубернтес, можем указать название сервиса kubernetes.default

## 3. Настройка ingress

Доступ к приложению будет осуществляться через ingress. Ingress устанавливается вместе с приложением, но для его корректной работы необходимо прописать ему адрес.
Для этого откроем `values.yaml`:

```bash
vi ~/xpaste/.helm/values.yaml
```

В переменной host необходимо указать DNS название, которое вы выдали сайту xpaste:

```diff
- host: xpaste.s<Ваш номер логина>.edu.slurm.io
+ host: xpaste.s000001.edu.slurm.io
```

Сохраняем все изменения и пушим их в gitlab. Для этого необходимо выполнить команды:

```bash
cd ~/xpaste
git add .
git commit -am "Add CI/CD config"
git push
```

## 4. Переключаемся в namespace приложения

Наше приложение xpaste устанавливается в другой namespace `xpaste-development`.
Для удобства работы, чтобы не набирать каждый раз опцию `--namespace` изменим namespace, который kubectl использует по умолчанию:

```bash
kubectl config set-context --current --namespace=xpaste-development
```

## 5. Проверка результата

Для проверки результата необходимо перейти в Gitlab в раздел `ci/cd -> pipelines` форка проекта xpaste.
Можно воспользоваться прямой ссылкой: `https://gitlab.com/<наименование своего нэймспэйса>/xpaste/pipelines`. `<наименование своего нэймспэйса>` необходимо заменить на свой каталог в гитлабе.

В результате все job должны закончиться без ошибок.

## 6.Открываем приложение в браузере

В браузере открываем URL: http://xpaste.s<Ваш номер логина>.edu.slurm.io. Открывать нужно в режиме `инкогнито`.
