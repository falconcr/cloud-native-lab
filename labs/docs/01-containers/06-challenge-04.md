Excelente. Aquí tienes dos retos (challenges) educativos, explicados paso a paso y en inglés, ideales para personas que están aprendiendo Docker **sin Compose**.
## 🔥 Challenge 4: Persistent Database with Volumes

**🧩 Story:**
You're running a PostgreSQL database container, but every time you delete it, the data disappears! 😩
Your mission is to **attach a volume** to keep the data alive — even if the container is gone.

---

### 🎯 Goal:

1. Start a PostgreSQL container with a volume.
2. Create a table and insert some data.
3. Delete the container.
4. Start a new container **with the same volume**.
5. Show that the data is still there. 🎉

---

### 🪜 Steps suggested but if something is bad please fix (I am giving a pieces of advice):

#### ✅ 1. Create a volume

```bash
docker volume create pgdata
```

#### ✅ 2. Run a Postgres container using the volume

```bash
docker run -d \
  --name mydb \
  -e POSTGRES_USER=admin \
  -e POSTGRES_PASSWORD=secret \
  -e POSTGRES_DB=mydb \
  -v pgdata:/var/lib/postgresql/data \
  postgres:14
```

#### ✅ 3. Insert some data

```bash
docker exec -it mydb psql -U admin -d mydb
```

Inside the `psql` shell:

```sql
CREATE TABLE students (id SERIAL PRIMARY KEY, name TEXT);
INSERT INTO students (name) VALUES ('Alice');
\q
```

#### ✅ 4. Delete the container

```bash
docker rm -f mydb
```

#### ✅ 5. Start a new Postgres container (same volume)

```bash
docker run -d \
  --name newdb \
  -e POSTGRES_USER=admin \
  -e POSTGRES_PASSWORD=secret \
  -e POSTGRES_DB=mydb \
  -v pgdata:/var/lib/postgresql/data \
  postgres:14
```

#### ✅ 6. Check the data

```bash
docker exec -it newdb psql -U admin -d mydb
```

```sql
SELECT * FROM students;
```

🎉 You should still see `Alice`.
**Success! You made your database persistent.**