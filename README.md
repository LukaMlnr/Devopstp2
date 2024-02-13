<p align="center">
  <a href="https://www.docker.com/">
    <img src="https://www.docker.com/wp-content/uploads/2023/08/logo-dont-spacing.svg" alt="Logo_docker" width=120 height=120>
  </a>

  <h2 align="center">Docker TP2</h2>

  <p align="center">
    DevOps
    <br>
  </p>
</p>

<br>

# Question 2

la commande ```bash --only=production``` permet de n'installer que les dépendances nécessaires (celles de production).

```sql
FROM node:12-alpine3.9
WORKDIR /app
COPY package.json package-lock.json ./
RUN npm install --only=production
COPY . .
RUN npm run build
CMD ["node", "src/index.js"]
```

# Question 3 

```bash
docker run -p 3000:3000 ma_super_app
```

### Résultats 

```bash
tp-docker-2 % docker build -t ma_super_app .
[+] Building 4.5s (9/9) FINISHED                                                                                                         docker:desktop-linux
 => [internal] load build definition from Dockerfile                                                                                                     0.0s
 => => transferring dockerfile: 194B                                                                                                                     0.0s
 => [internal] load metadata for docker.io/library/node:14-alpine                                                                                        0.4s
 => [internal] load .dockerignore                                                                                                                        0.0s
 => => transferring context: 2B                                                                                                                          0.0s
 => [1/4] FROM docker.io/library/node:14-alpine@sha256:434215b487a329c9e867202ff89e704d3a75e554822e07f3e0c0f9e606121b33                                  3.2s
 => => resolve docker.io/library/node:14-alpine@sha256:434215b487a329c9e867202ff89e704d3a75e554822e07f3e0c0f9e606121b33                                  0.0s
 => => sha256:434215b487a329c9e867202ff89e704d3a75e554822e07f3e0c0f9e606121b33 1.43kB / 1.43kB                                                           0.0s
 => => sha256:3380ed827b250d2db2bd38c15f090af2b303b3c9ebb42f5927cb5b9adeea7a6e 1.16kB / 1.16kB                                                           0.0s
 => => sha256:d561716d42b6a03639723c382c62977347ed62f13925e836614583253308e6c3 6.45kB / 6.45kB                                                           0.0s
 => => sha256:c41833b44d910632b415cd89a9cdaa4d62c9725dc56c99a7ddadafd6719960f9 3.26MB / 3.26MB                                                           0.3s
 => => sha256:683339ce8d6b9be2ca150a8de67b895e20ea5594b91d3911c95b0b8fea3e314c 36.99MB / 36.99MB                                                         1.6s
 => => sha256:4cf6a83c0e2af3c780abcda02cc33f9e812fdcb40b610ed1838281cc9ab94ec8 2.43MB / 2.43MB                                                           0.7s
 => => extracting sha256:c41833b44d910632b415cd89a9cdaa4d62c9725dc56c99a7ddadafd6719960f9                                                                0.1s
 => => sha256:686172e40c38722891b4004f55f6447548c8367968ac523a612591e0d92f9db3 447B / 447B                                                               0.5s
 => => extracting sha256:683339ce8d6b9be2ca150a8de67b895e20ea5594b91d3911c95b0b8fea3e314c                                                                1.4s
 => => extracting sha256:4cf6a83c0e2af3c780abcda02cc33f9e812fdcb40b610ed1838281cc9ab94ec8                                                                0.0s
 => => extracting sha256:686172e40c38722891b4004f55f6447548c8367968ac523a612591e0d92f9db3                                                                0.0s
 => [internal] load build context                                                                                                                        0.0s
 => => transferring context: 491B                                                                                                                        0.0s
 => [2/4] WORKDIR /app                                                                                                                                   0.1s
 => [3/4] RUN npm install --only=production                                                                                                              0.7s
 => [4/4] COPY . .                                                                                                                                       0.0s
 => exporting to image                                                                                                                                   0.0s
 => => exporting layers                                                                                                                                  0.0s
 => => writing image sha256:4d7ac7ff611637fcf32a50b2873f9c8ebb31f5152532acb872f38a66b9d63420                                                             0.0s
 => => naming to docker.io/library/ma_super_app 
```

# Question 4

```bash
version: '3.9'

services:
  node:
    image: ma_super_app
    build: .
    ports:
      - "3000:3000"
    environment:
      - DATABASE_HOST=mysql
      - DATABASE_PORT=3306
      - DATABASE_USERNAME=lucas
      - DATABASE_PASSWORD=password
      - DATABASE_NAME=my_database

  mysql:
    image: mysql:latest
    environment:
      - MYSQL_ROOT_PASSWORD=password
      - MYSQL_DATABASE=my_database
      - MYSQL_USER=lucas
      - MYSQL_PASSWORD=password
    ports:
      - "3306:3306"

```

