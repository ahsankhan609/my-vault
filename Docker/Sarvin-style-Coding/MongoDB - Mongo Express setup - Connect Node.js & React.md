![Pasted image 20260603171634.png](../../Attachments/Pasted%20image%2020260603171634.png)

here, our task is to read and write simple application to [[MongoDB]] database

```bash
docker pull mongo:noble
```

```bash
docker pull mongo-express:1.0.2-20-alpine3.19
```

#### list all docker networks available on our system

```bash
docker netwrok ls
```

#### create own network

```bash
docker network create NETWORK_NAME
```