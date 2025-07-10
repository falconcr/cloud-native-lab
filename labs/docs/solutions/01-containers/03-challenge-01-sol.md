# 🧩 Challenge 1 Solution – Create a Simple App with Docker (Node.js + Dockerfile)

In this challenge, we’re building a Docker container to run a basic Node.js web server that responds with **“Welcome to CloudBakery!”**.

---

## 🧠 What You’ll Learn

- How to write a simple Node.js server
- How to write a Dockerfile from scratch
- How to build and run a Docker image locally

---

## 🥣 Step 1 – Set up the Node.js app

Create a file called `server.js`:

```js
const http = require('http');

const server = http.createServer((req, res) => {
  res.end('Welcome to CloudBakery!');
});

server.listen(3000, () => {
  console.log('Server running at http://localhost:3000');
});

