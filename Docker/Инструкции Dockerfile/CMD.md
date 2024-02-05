Инструкция [CMD](https://docs.docker.com/engine/reference/builder/#cmd) предоставляет Docker команду, которую нужно выполнить при запуске контейнера. Результаты выполнения этой команды не добавляются в образ во время его сборки. В примере с помощью этой команды запускается скрипт `my_script.py` во время выполнения контейнера.  
  
Вот ещё кое-что, что нужно знать об инструкции `CMD`:  
- В одном файле Dockerfile может присутствовать лишь одна инструкция `CMD`. Если в файле есть несколько таких инструкций, система проигнорирует все кроме последней.
- Инструкция `CMD` может иметь exec-форму. Если в эту инструкцию не входит упоминание исполняемого файла, тогда в файле должна присутствовать инструкция [[ENTRYPOINT]]. В таком случае обе эти инструкции должны быть представлены в формате `JSON`.
- Аргументы командной строки, передаваемые `docker run`, переопределяют аргументы, предоставленные инструкции `CMD` в Dockerfile.

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