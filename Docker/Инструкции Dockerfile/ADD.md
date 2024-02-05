Инструкция [ADD](https://docs.docker.com/engine/reference/builder/#add) позволяет решать те же задачи, что и [[COPY]], но с ней связана ещё пара вариантов использования. Так, с помощью этой инструкции можно добавлять в контейнер файлы, загруженные из удалённых источников, а также распаковывать локальные .tar-файлы.  
В примере инструкция `ADD` была использована для копирования файла, доступного по URL, в директорию контейнера `my_app_directory`. Надо отметить, однако, что [документация Docker](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/) не рекомендует использование подобных файлов, полученных по URL, так как удалить их нельзя, и так как они увеличивают размер образа.  
  
Кроме того, [документация](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/#add-or-copy) предлагает везде, где это возможно, вместо инструкции `ADD` использовать инструкцию [[COPY]] для того, чтобы сделать файлы Dockerfile понятнее. Полагаю, команде разработчиков Docker стоило бы объединить `ADD` и `COPY` в одну инструкцию для того, чтобы тем, кто создаёт образы, не приходилось бы помнить слишком много инструкций.  
  
Обратите внимание на то, что инструкция `ADD` содержит символ разрыва строки — `\`. Такие символы используются для улучшения читабельности длинных команд путём разбиения их на несколько строк.

```
FROM python:3.7.2-alpine3.8
LABEL maintainer="jeffmshale@gmail.com"
ENV ADMIN="jeff"
RUN apk update && apk upgrade && apk add bash
COPY . ./app
ADD https://raw.githubusercontent.com/discdiver/pachy-vid/master/sample_vids/vid1.mp4 \
/my_app_directory
RUN ["mkdir", "/a_directory"]
CMD ["python", "./my_script.py"]
```