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

