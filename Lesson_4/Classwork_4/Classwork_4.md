`mkdir cowsay_test` <br>
`cd cowsay_test` <br>
`nano Dockerfile` <br>

```Script
FROM ubuntu:22.10
RUN apt-get update && \
    apt-get install -y cowsay && \
    ln -s /usr/games/cowsay /usr/bin/cowsay && \
    rm -rf /var/lib/apt/lists/*
CMD ["cowsay"]
```

`cd /home/slava/cowsay_test/` <br>
`docker build -t cowsaytest .` <br>
`docker run --name cowsay_test -h cowsay cowsaytest` <br>
`docker exec cowsay_test cowsay "hi"` <br>

```Script
FROM ubuntu:22.10
RUN apt update && \
    apt full-upgrade -y && \
    apt install nginx -y && \
    rm -rf /var/lib/apt/lists/*
EXPOSE 8082
ENTRYPOINT ["nginx", "-g", "daemon off;"]
```

