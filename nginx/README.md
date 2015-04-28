
1. Build container

  ```
  docker build -t zemirco/nginx .
  ```

2. Run container

  ```
  docker run -p 80:80 -d zemirco/nginx
  ```

3. Stop container

  ```
  docker stop <id_short>
  ```
