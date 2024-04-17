# Домашнее задание к занятию «GitLab» - Балашова Екатерина 
---

### Задание 1

**Что нужно сделать:**

1. Разверните GitLab локально, используя Vagrantfile и инструкцию, описанные в [этом репозитории](https://github.com/netology-code/sdvps-materials/tree/main/gitlab).   
2. Создайте новый проект и пустой репозиторий в нём.
3. Зарегистрируйте gitlab-runner для этого проекта и запустите его в режиме Docker. Раннер можно регистрировать и запускать на той же виртуальной машине, на которой запущен GitLab.

В качестве ответа в репозиторий шаблона с решением добавьте скриншоты с настройками раннера в проекте.

### Решение 1

![image](https://github.com/k1tit/gitlab-ci-hw/assets/165839233/6e4927a6-fbb3-489d-bfb4-e88c627944b1)
![image](https://github.com/k1tit/gitlab-ci-hw/assets/165839233/5bdc0270-0b39-4981-bb7f-165c73e9cdca)
![image](https://github.com/k1tit/gitlab-ci-hw/assets/165839233/1af0c41c-00be-45ea-a2c4-7acb474f2812)


---

### Задание 2

**Что нужно сделать:**

1. Запушьте [репозиторий](https://github.com/netology-code/sdvps-materials/tree/main/gitlab) на GitLab, изменив origin. Это изучалось на занятии по Git.
2. Создайте .gitlab-ci.yml, описав в нём все необходимые, на ваш взгляд, этапы.

В качестве ответа в шаблон с решением добавьте: 
   
 * файл gitlab-ci.yml для своего проекта или вставьте код в соответствующее поле в шаблоне; 
 * скриншоты с успешно собранными сборками.

 ### Решение 2

 gitlab-ci.yml
 
```
stages:
  - test
  - static-analysis
  - build

test:
  stage: test
  image: golang:1.16
  script: 
   - go test .

static-analysis:
 stage: test
 image:
  name: sonarsource/sonar-scanner-cli
  entrypoint: [""]
 variables:
 script:
  - sonar-scanner -Dsonar.projectKey=checkeray -Dsonar.sources=. -Dsonar.host.url=http://192.200.0.104:9000 -Dsonar.login=sqp_d7488143f45cd61c4d8de98b972ddf49ab52f910

build:
  stage: build
  image: docker:latest
  script:
   - docker build . --tag gitlab-ci:latest
```
![image](https://github.com/k1tit/gitlab-ci-hw/assets/165839233/e978b29f-d79e-44f3-8c50-6901901820ab)
![image](https://github.com/k1tit/gitlab-ci-hw/assets/165839233/36d33661-29b7-4434-bf66-d2f367808b3b)

