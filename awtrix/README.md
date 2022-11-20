# Home Assistant Add-on: Awtrix


### Dockerfile
```
FROM amd64/openjdk:19-alpine

COPY entrypoint.sh /entrypoint.sh

COPY awtrix.jar /awtrix.jar

RUN chmod +x /entrypoint.sh
#EXPOSE 7000
#EXPOSE 7001
WORKDIR /data
CMD /entrypoint.sh

#ENTRYPOINT ["tail", "-f", "/dev/null"]
```


### Entrypoint
```
#!/bin/sh

FILE=/data/awtrix.jar
if [[ -f "$FILE" ]]; then
echo "$FILE exists."
else
echo "$FILE do not exist exists. Copying"
cp /awtrix.jar /data/awtrix.jar
fi

java -jar /data/awtrix.jar
```



### build and push
```
docker build -t awtrix .
docker image tag awtrix jokep/awtrix:latest
docker push jokep/awtrix:latest
```

