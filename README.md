
##### Install Docker

##### Create image from `Dockerfile`

```
docker build --tag zemirco/go .
```

##### Run image

```
docker run -p 8080:8080 -d zemirco/go
```

#### On Mac

##### Get IP address

```
boot2docker ip
```
