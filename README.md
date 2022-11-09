# Модуль 3.1 Docker

Целью данного модуля является знакомство с Docker и предоставляемыми им средствами для сборки образов и запуска контейнеров.   
В ходе выполнения этого практического задания, мы рассмотрим:
- написание Dockerfile;
- использование команды docker build;
- применение лучших практик по написанию Dockerfile;
- оптимизацию процесса сборки;
- использование команд управления контейнерами и просмотра их статуса;
- использование volumes;

## Предварительная настройка

1. Предполагается, что вы выполнили [задание по модулю Git](https://github.com/digital-academy-devops/git-module) и имеете опыт использования git и 
настроенную среду для работы с CLI-утилитами (консоль в Linux/MacOS X, GitBash или виртуальную машину в Windows).
1. [Установите](https://docs.docker.com/engine/install/) и запустите Docker engine.

## Задание

В качестве тестового приложения, используем [пример](https://github.com/digital-academy-devops/git-example) реализации [задания](https://github.com/digital-academy-devops/git-module) по модулю Git. 

1. Создайте собственный форк репозитория с примером.
1. Добавьте Dockerfile для сборки следующих образов. 
    1. **Образ 1**, который содержит:
        - Необходимые файлы и утилиты для осуществления сборки версии резюме внутри контейнера.
        - Использует в качестве основной команды `task` и позволяет выполнять автоматизированные задачи при запуске контейнера.
        - При запуске контейнера без дополнительных агрументов, выполняет задачу сборки.
    1. **Образ 2**, который содержит только собранную версию резюме в формате HTML и экспортирует её для использования в других контейнерах. 
1. Автоматизируйте задачу сборки образов.
1. Оптимизируйте процесс сборки образов.

## Вопросы

- Предложите вариант того, как можно создать fork только средствами Git, без использования фукнкционала Github (`Fork` > `Create a new fork`)
- Укажите, в чём разница `ENTRYPOINT` и `CMD`, и когда предпочтительней их использовать.
- Укажите в чём разница `ADD` и `COPY`, и когда предпочтительней их использовать.

## Рекомендации

- Для ответов на вопросы, используйте **Issues** и механизм упоминаний (https://www.google.com/search?q=github+mentions) пользователя `digital-academy-devops` для отправки нотификаций о готовности ответа к проверке.
- Выполнение всех этапов задания необходимо осуществлять в рамках одной ветки.  
- **Pull request** для ветки не обязательно должен быть создан по завершении работы и полной готовности кода к резензированию (code review). Вы можете создать PR в любой момент при необходимости получения комментариев - задавайте вопрос в комментариях к своему коду и адресуйте его `digital-academy-devops`.
- По завершении работы и готовности к code review, убедитесь что вы завершили (resolve conversations) все ветки обсуждений и укажите в комментариях к PR что он готов к ревью.

> **На заметку**
> В платной версии GitHub, для существует возможность создать набросок PR (Pull request Draft), позволяющий получить обратную связь по ходу работы над задачей, а по завершении опубликовать готовый PR из этого наброска.

## Пояснения
- Минимальный набор необходимых [инструкций Dockerfile](https://docs.docker.com/engine/reference/builder/) для изучения:
  - [FROM](https://docs.docker.com/engine/reference/builder/#from)
  - [COPY](https://docs.docker.com/engine/reference/builder/#copy)
  - [ADD](https://docs.docker.com/engine/reference/builder/#add)
  - [ENTRYPOINT](https://docs.docker.com/engine/reference/builder/#entrypoint)
  - [CMD](https://docs.docker.com/engine/reference/builder/#cmd)
  - [WORKDIR](https://docs.docker.com/engine/reference/builder/#workdir)
  - [RUN](https://docs.docker.com/engine/reference/builder/#run)
  - [VOLUME](https://docs.docker.com/engine/reference/builder/#volume)
  - [LABEL](https://docs.docker.com/engine/reference/builder/#label)
  - [USER](https://docs.docker.com/engine/reference/builder/#user)
  - [ENV](https://docs.docker.com/engine/reference/builder/#env)
  - [ARG](https://docs.docker.com/engine/reference/builder/#arg)
- Для сборки обоих образов, используйте один Dockerfile и [milti-stage build](https://docs.docker.com/build/building/multi-stage/).
- Автоматизация сборки осуществляется средствами Taskfile.
- Оптимизация, в первую очередь, включает в себя:
  - сокращение размера образа (используйте [docker history](https://docs.docker.com/engine/reference/commandline/history/) для анализа размера слоёв)
  - максимальное использование кэша при изменении исходного кода приложения и повторной сборки.
