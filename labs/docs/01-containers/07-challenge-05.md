
## 📡 Challenge 5: Networking — Containers That Can Talk (and Can’t)

**🧩 Story:**
You have two containers: a backend and a database. You want them to talk to each other. But someone tries to connect from a third container that’s *not* in the network — and it fails. Why? 🔒

---

### 🎯 Goal:

1. Create a custom Docker network.
2. Launch two containers (`app` and `db`) inside it.
3. Test communication between them using hostnames.
4. Start a third container outside that network.
5. Show it **cannot** access the others.

---

### 🪜 Steps:

#### ✅ 1. Create a custom network

```bash
docker network create app-network
```

#### ✅ 2. Start the DB container

```bash
docker run -d \
  --name db \
  --network app-network \
  -e POSTGRES_USER=admin \
  -e POSTGRES_PASSWORD=secret \
  -e POSTGRES_DB=mydb \
  postgres:14
```

#### ✅ 3. Start a fake app container in the same network

```bash
docker run -dit --name app --network app-network alpine sh
```

Install a tool to test connectivity:

```bash
docker exec -it app sh
apk add --no-cache postgresql-client
psql -h db -U admin -d mydb
```

➡️ You should be able to connect! ✅

---

#### 🚫 4. Start another container (outside the network)

```bash
docker run -dit --name outsider alpine sh
```

Try to ping or connect to `db`:

```bash
docker exec -it outsider sh
ping db
```

🚫 It will fail: `ping: bad address 'db'`

The container is **not in the same network**, so Docker’s internal DNS can’t resolve `db`.

---

### ✅ Bonus Tip:

If you want the outsider container to join the network after being created:

```bash
docker network connect app-network outsider
```

Now test again:

```bash
docker exec -it outsider sh
ping db
```

➡️ It works now.

---

> 🔁 *Quick Refresher:* Need a recap? Revisit the lesson on [Container Networking](02-docker.md#4-container-networking-and-volumes).
