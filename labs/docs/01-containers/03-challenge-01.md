## 🧩 **Challenge 1: The Mystery Cake (Docker CLI & Dockerfile)**

**Story:**
You just got hired at a virtual bakery 🍰. Your first task? Make a container image that runs a simple Node.js server that says `Welcome to CloudBakery!` when you visit it in the browser.

**Clues & Tips:**

* Start from a base image like `node:18`.
* Copy the source files (`server.js`, `package.json`) into the image.
* Install dependencies with `npm install`.
* Set the command: `node server.js`.
* Don’t forget to expose port 3000 and map it in `docker run`.

**Try:**

```bash
docker build -t cloudbakery .
docker run -p 3000:3000 cloudbakery
```

🧠 *Hint:* If you're not sure how the `Dockerfile` should look, search for a minimal example with `node`.
🔁 *Quick Refresher:* Need a recap? Revisit the lesson on [Docker CLI & Dockerfile Syntax](02-docker.md#1-docker-cli-dockerfile-syntax).