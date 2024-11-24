Инструкция [RUN](https://docs.docker.com/engine/reference/builder/#run) позволяет создать слой во время сборки образа. После её выполнения в образ добавляется новый слой, его состояние фиксируется. Инструкция `RUN` часто используется для установки в образы дополнительных пакетов. В примере инструкция `RUN apk update && apk upgrade` сообщает Docker о том, что системе нужно обновить пакеты из базового образа. Вслед за этими двумя командами идёт команда `&& apk add bash`, указывающая на то, что в образ нужно установить bash.  
  
То, что в командах выглядит как `apk` — это сокращение от [Alpine Linux package manager](https://www.cyberciti.biz/faq/10-alpine-linux-apk-command-examples/) (менеджер пакетов Alpine Linux). Если вы используете базовый образ какой-то другой ОС семейства Linux, тогда вам, например, при использовании Ubuntu, для установки пакетов может понадобиться команда вида `RUN apt-get`. 

Инструкция `RUN` и схожие с ней инструкции — такие, как `CMD` и `ENTRYPOINT`, могут быть использованы либо в exec-форме, либо в shell-форме. Exec-форма использует синтаксис, напоминающий описание JSON-массива. Например, это может выглядеть так: `RUN ["my_executable", "my_first_param1", "my_second_param2"]`.  
  
В примере мы использовали shell-форму инструкции RUN в таком виде: `RUN apk update && apk upgrade && apk add bash`.  
  
Позже в нашем Dockerfile использована exec-форма инструкции `RUN`, в виде `RUN ["mkdir", "/a_directory"]` для создания директории. При этом, используя инструкцию в такой форме, нужно помнить о необходимости оформления строк с помощью двойных кавычек, как это принято в формате JSON.

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