# Домашнее задание к занятию "`Название занятия`" - `Фамилия и имя студента`


### Инструкция по выполнению домашнего задания

   1. Сделайте `fork` данного репозитория к себе в Github и переименуйте его по названию или номеру занятия, например, https://github.com/имя-вашего-репозитория/git-hw или  https://github.com/имя-вашего-репозитория/7-1-ansible-hw).
   2. Выполните клонирование данного репозитория к себе на ПК с помощью команды `git clone`.
   3. Выполните домашнее задание и заполните у себя локально этот файл README.md:
      - впишите вверху название занятия и вашу фамилию и имя
      - в каждом задании добавьте решение в требуемом виде (текст/код/скриншоты/ссылка)
      - для корректного добавления скриншотов воспользуйтесь [инструкцией "Как вставить скриншот в шаблон с решением](https://github.com/netology-code/sys-pattern-homework/blob/main/screen-instruction.md)
      - при оформлении используйте возможности языка разметки md (коротко об этом можно посмотреть в [инструкции  по MarkDown](https://github.com/netology-code/sys-pattern-homework/blob/main/md-instruction.md))
   4. После завершения работы над домашним заданием сделайте коммит (`git commit -m "comment"`) и отправьте его на Github (`git push origin`);
   5. Для проверки домашнего задания преподавателем в личном кабинете прикрепите и отправьте ссылку на решение в виде md-файла в вашем Github.
   6. Любые вопросы по выполнению заданий спрашивайте в чате учебной группы и/или в разделе “Вопросы по заданию” в личном кабинете.
   
Желаем успехов в выполнении домашнего задания!
   
### Дополнительные материалы, которые могут быть полезны для выполнения задания

1. [Руководство по оформлению Markdown файлов](https://gist.github.com/Jekins/2bf2d0638163f1294637#Code)

---

### Задание 1

`Приведите ответ в свободной форме........`


![alt text](https://github.com/SLzDevOps/netology-education-hw81/blob/main/Screenshot_463.png)
![alt text](https://github.com/SLzDevOps/netology-education-hw81/blob/main/Screenshot_464.png)
![alt text](https://github.com/SLzDevOps/netology-education-hw81/blob/main/Screenshot_465.png)
![alt text](https://github.com/SLzDevOps/netology-education-hw81/blob/main/Screenshot_466.png)
![alt text](https://github.com/SLzDevOps/netology-education-hw81/blob/main/Screenshot_467.png)
![alt text](https://github.com/SLzDevOps/netology-education-hw81/blob/main/Screenshot_468.png)
![alt text](https://github.com/SLzDevOps/netology-education-hw81/blob/main/Screenshot_469.png)
![alt text](https://github.com/SLzDevOps/netology-education-hw81/blob/main/Screenshot_470.png)
![alt text](https://github.com/SLzDevOps/netology-education-hw81/blob/main/Screenshot_471.png)
![alt text](https://github.com/SLzDevOps/netology-education-hw81/blob/main/Screenshot_472.png)
![alt text](https://github.com/SLzDevOps/netology-education-hw81/blob/main/Screenshot_473.png)


---

### Задание 2

![alt text](https://github.com/SLzDevOps/netology-education-hw81/blob/main/Screenshot_474.png)
![alt text](https://github.com/SLzDevOps/netology-education-hw81/blob/main/Screenshot_475.png)
![alt text](https://github.com/SLzDevOps/netology-education-hw81/blob/main/Screenshot_476.png)
![alt text](https://github.com/SLzDevOps/netology-education-hw81/blob/main/Screenshot_477.png)
![alt text](https://github.com/SLzDevOps/netology-education-hw81/blob/main/Screenshot_478.png)
![alt text](https://github.com/SLzDevOps/netology-education-hw81/blob/main/Screenshot_479.png)
![alt text](https://github.com/SLzDevOps/netology-education-hw81/blob/main/Screenshot_480.png)
![alt text](https://github.com/SLzDevOps/netology-education-hw81/blob/main/Screenshot_481.png)
![alt text](https://github.com/SLzDevOps/netology-education-hw81/blob/main/Screenshot_482.png)
![alt text](https://github.com/SLzDevOps/netology-education-hw81/blob/main/Screenshot_483.png)
![alt text](https://github.com/SLzDevOps/netology-education-hw81/blob/main/Screenshot_484.png)
![alt text](https://github.com/SLzDevOps/netology-education-hw81/blob/main/Screenshot_485.png)


---

### Задание 3


Взял в яндексе 2 вм, одна сразу с gitlab, выполнил все согласно ДЗ

Главные струдности - после перезапуска gitlab и вм runner получили други ip от яндекса
долго мучался почему гитлаб лезет по url с ip ...140, хотя у меня он виден на 204 и повершел заходит по ssh.
гугл и правка  /etc/gitlab/gitlab.rb, строка - external_url 'http://89.169.177.204'

после зависла машина runner, решил добаваить 2 проца и 2гб, заспуск и новый ip - переделка runner для gitlab командами с нуля(вот тут я и словил косяк с двумя runner в конфиге)

вот тут то я и просидел 3 часа ищя ошибку ERROR: error during connect: Head "http://docker:2375/_ping": dial tcp: lookup docker on 10.0.2.2:53: 

соответственно новый runner создался без строки сокета
volumes = ["/cache", "/var/run/docker.sock:/var/run/docker.sock"]
и я это ковырял... ... ... ...

когда уже поправил, удалил и перезапустил все стало хорошо! 

```
Поле для вставки кода...
stages:
  - test
  - sonar_test
  - build

test:
  stage: test
  image: golang:1.17
  script: 
   - go test .
  tags:
    - avf-runner

static-analysis_job:
 stage: sonar_test
 image:
  name: sonarsource/sonar-scanner-cli
  entrypoint: [""]
 variables:
 script:
  - sonar-scanner -Dsonar.projectKey=avf-netology -Dsonar.sources=. -Dsonar.host.url=http://51.250.20.179:9000 -Dsonar.login=sqp_f540116b9ebef0546166b4fea8f303c4683bbae1
 tags:
  - avf-runner



build:
  stage: build
  image: docker:latest
  script:
   - docker build .
  tags:
   - avf-runner

```
`При необходимости прикрепитe сюда скриншоты
![alt text](https://github.com/SLzDevOps/netology-education-hw81/blob/main/Screenshot_488.png)
![alt text](https://github.com/SLzDevOps/netology-education-hw81/blob/main/Screenshot_488.png)
![alt text](https://github.com/SLzDevOps/netology-education-hw81/blob/main/Screenshot_489.png)
![alt text](https://github.com/SLzDevOps/netology-education-hw81/blob/main/Screenshot_490.png)
![alt text](https://github.com/SLzDevOps/netology-education-hw81/blob/main/Screenshot_491.png)
![alt text](https://github.com/SLzDevOps/netology-education-hw81/blob/main/Screenshot_492.png)
![alt text](https://github.com/SLzDevOps/netology-education-hw81/blob/main/Screenshot_493.png)
![alt text](https://github.com/SLzDevOps/netology-education-hw81/blob/main/Screenshot_494.png)
![alt text](https://github.com/SLzDevOps/netology-education-hw81/blob/main/Screenshot_495.png)
![alt text](https://github.com/SLzDevOps/netology-education-hw81/blob/main/Screenshot_496.png)
![alt text](https://github.com/SLzDevOps/netology-education-hw81/blob/main/Screenshot_497.png)
![alt text](https://github.com/SLzDevOps/netology-education-hw81/blob/main/Screenshot_498.png)
![alt text](https://github.com/SLzDevOps/netology-education-hw81/blob/main/Screenshot_499.png)
![alt text](https://github.com/SLzDevOps/netology-education-hw81/blob/main/Screenshot_500.png)
![alt text](https://github.com/SLzDevOps/netology-education-hw81/blob/main/Screenshot_501.png)
![alt text](https://github.com/SLzDevOps/netology-education-hw81/blob/main/Screenshot_502.png)
![alt text](https://github.com/SLzDevOps/netology-education-hw81/blob/main/Screenshot_503.png)
![alt text](https://github.com/SLzDevOps/netology-education-hw81/blob/main/Screenshot_504.png)
![alt text](https://github.com/SLzDevOps/netology-education-hw81/blob/main/Screenshot_505.png)



### Задание 4

`Приведите ответ в свободной форме........`

1. `Заполните здесь этапы выполнения, если требуется ....`
2. `Заполните здесь этапы выполнения, если требуется ....`
3. `Заполните здесь этапы выполнения, если требуется ....`
4. `Заполните здесь этапы выполнения, если требуется ....`
5. `Заполните здесь этапы выполнения, если требуется ....`
6. 

```
Поле для вставки кода...
....
....
....
....
```

`При необходимости прикрепитe сюда скриншоты
![alt text](https://github.com/SLzDevOps/netology-education-hw81/blob/main/Screenshot_488.png)
![alt text](https://github.com/SLzDevOps/netology-education-hw81/blob/main/Screenshot_488.png)
![alt text](https://github.com/SLzDevOps/netology-education-hw81/blob/main/Screenshot_489.png)
![alt text](https://github.com/SLzDevOps/netology-education-hw81/blob/main/Screenshot_490.png)
![alt text](https://github.com/SLzDevOps/netology-education-hw81/blob/main/Screenshot_491.png)
![alt text](https://github.com/SLzDevOps/netology-education-hw81/blob/main/Screenshot_492.png)
![alt text](https://github.com/SLzDevOps/netology-education-hw81/blob/main/Screenshot_493.png)
![alt text](https://github.com/SLzDevOps/netology-education-hw81/blob/main/Screenshot_494.png)
![alt text](https://github.com/SLzDevOps/netology-education-hw81/blob/main/Screenshot_495.png)
![alt text](https://github.com/SLzDevOps/netology-education-hw81/blob/main/Screenshot_496.png)
![alt text](https://github.com/SLzDevOps/netology-education-hw81/blob/main/Screenshot_497.png)
![alt text](https://github.com/SLzDevOps/netology-education-hw81/blob/main/Screenshot_498.png)
![alt text](https://github.com/SLzDevOps/netology-education-hw81/blob/main/Screenshot_499.png)
![alt text](https://github.com/SLzDevOps/netology-education-hw81/blob/main/Screenshot_500.png)
![alt text](https://github.com/SLzDevOps/netology-education-hw81/blob/main/Screenshot_501.png)
![alt text](https://github.com/SLzDevOps/netology-education-hw81/blob/main/Screenshot_502.png)
![alt text](https://github.com/SLzDevOps/netology-education-hw81/blob/main/Screenshot_503.png)
![alt text](https://github.com/SLzDevOps/netology-education-hw81/blob/main/Screenshot_504.png)
![alt text](https://github.com/SLzDevOps/netology-education-hw81/blob/main/Screenshot_505.png)

