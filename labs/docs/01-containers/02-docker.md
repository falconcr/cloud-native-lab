## 🐳 **1. Docker CLI & Dockerfile Syntax**

Docker is like a **kitchen**, and the `Dockerfile` is your **recipe**.

Imagine you’re a chef. You don’t cook freestyle every time — you follow a recipe. That’s exactly what a `Dockerfile` does: it tells Docker how to **build your application image**.

* First, you **choose a base image** — like picking the type of kitchen you’ll use (e.g., `node:18` or `python:3.11-slim`).
* Then you add the **ingredients** — your code and dependencies.
* Finally, you define the **command to run the app**, like turning on the stove.

To **build** the image from that recipe, you use `docker build`. That creates a new container image, kind of like baking a cake and wrapping it up for delivery.

Once the image is ready, you can run it using `docker run`, which launches your app inside an isolated container — like cooking and serving the meal.

👉 To try this: write a `Dockerfile`, build it, and run it. Example:

```bash
docker build -t myapp .
docker run -p 3000:3000 myapp
```

📚 [Learn more (official docs)](https://docs.docker.com/engine/reference/builder/)

---

## ⚙️ **2. Docker Compose for Multi-Service Setup**

Most real-world apps are not solo artists — they’re **bands**. Your backend is the singer 🎤, your database is the drummer 🥁, and maybe your frontend is the DJ 🎧.

Managing all these with `docker run` manually would be chaotic — like having every musician show up at a different time with no plan.

That’s where `docker-compose` comes in. It’s your **conductor**.

With a `docker-compose.yml` file, you define multiple services — each one a container — and describe how they work together:

* Which image or Dockerfile to use
* Which ports to expose
* What environment variables or volumes to include
* How the services connect to each other internally

You then launch all services at once with just:

```bash
docker-compose up
```

They’re all orchestrated and networked automatically — just like a band in sync.

📚 [Explore the Compose docs](https://docs.docker.com/compose/)

---

## 📦 **3. Base Image Selection vs Multistage Builds**

When building something (like a house), you don’t bring the entire warehouse of tools to the construction site — just what you need.

In Docker, the **base image** is your starting toolbox. Some are small (`alpine`, `slim`), and some are big (with compilers and build tools). Using a lighter image makes your app faster to download and start, and **reduces attack surface**.

A **multistage build** is a way to use all your tools during the build stage (installing, compiling), but only **ship the final clean result**.

For example:

1. First stage: build the frontend using Node.js
2. Second stage: copy the built files into a tiny Nginx container

This results in a small, production-ready image without any of the dev tools inside.

```Dockerfile
# Stage 1 - build
FROM node:18 as builder
WORKDIR /app
COPY . .
RUN npm install && npm run build

# Stage 2 - run
FROM nginx:alpine
COPY --from=builder /app/dist /usr/share/nginx/html
```

📚 [Multistage builds guide](https://docs.docker.com/build/building/multi-stage/)

---

## 🌐 **4. Container Networking and Volumes**

Think of each container like a **room in a house**.

* **Ports** are the doors — they allow things to go in and out.
* **Networks** are like walkie-talkies between rooms — containers can talk to each other over a shared private network.
* **Volumes** are shared cabinets — places to store things that shouldn’t be lost when the container is deleted (like databases or uploaded files).

By default, containers are isolated. But with Docker Compose or custom networks, they can talk to each other by name (e.g., `db:5432`).

Volumes are created to make data **persist**. For example, if you delete a container, but want the database data to survive, you mount a volume like this:

```yaml
volumes:
  - dbdata:/var/lib/postgresql/data
```

This way, even if your database container crashes or is updated, the data stays safe.

📚 [Docker networking docs](https://docs.docker.com/network/)
📚 [Docker volumes docs](https://docs.docker.com/storage/volumes/)

---

## 🧰 **5. Debugging Containers (exec, logs, inspect)**

A container is like a **sealed box** running your application. When something doesn’t work, you need to become a **mechanic** with the right tools.

* Use `docker logs` to see what’s going wrong — it’s like reading the **warning lights** on a car dashboard.
* Use `docker exec -it <container> /bin/sh` to **get inside the container** — like opening the hood to check things directly.
* Use `docker inspect` to get **detailed information** about the container — the full spec sheet, network, volumes, environment variables, and more.

When your app doesn’t start or behaves strangely, this is how you **investigate**.

```bash
docker logs myapp
docker exec -it myapp /bin/sh
docker inspect myapp
```

These tools are **essential** for real-world debugging and help you build the habit of not guessing — but inspecting and understanding.

📚 [Official debugging docs](https://docs.docker.com/config/containers/logging/)

