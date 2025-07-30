# 🧩 Challenge 1 Solution – Create a Simple App with Docker (Node.js + Dockerfile)

In this challenge, we’re building a Docker container to run a basic Node.js web server that responds with **“Welcome to CloudBakery!”**.

We'll learn:

- How to write a simple Node.js server
- How to write a `Dockerfile` from scratch
- How to build and run a Docker image locally using Docker CLI

---

## Step 1 – Set up the Node.js app

Before we can containerize anything, we need something to containerize!

In this step, we'll write a simple HTTP server using Node.js. This server will respond with the message **"Welcome to CloudBakery!"** whenever someone accesses it from their browser.

Create a file called `server.js` with the following code:

    const http = require('http');

    const server = http.createServer((req, res) => {
    res.end('Welcome to CloudBakery!');
    });

    server.listen(3000, () => {
    console.log('Server running at http://localhost:3000');
    });
 
 > In this file we use Node.js’ built-in `http` module (no frameworks or libraries). The server listens on `port 3000`. Every request gets the same response: `"Welcome to CloudBakery!"`.

Now, create a file called `package.json` to define your app’s metadata and entry point:

    {
    "name": "cloudbakery",
    "version": "1.0.0",
    "main": "server.js",
    "scripts": {
        "start": "node server.js"
    }
    }
    
> We don’t need any external dependencies here, but having a package.json is still helpful:
> It ensures Docker can run npm install (even if there’s nothing to install).
> It lets you define the default command (npm start or node server.js).
> It's standard practice for Node.js apps, even minimal ones.
> We'll use `npm install` later inside the container, so make sure this file exists.

With both files in place, you now have a self-contained Node.js app that can run locally, and be packaged into a container in the next step.

## Step 2 – Write the Dockerfile

Create a minimal Dockerfile that follows the instructions from the challenge:

    FROM node:18

    WORKDIR /app

    COPY package.json .
    COPY server.js .

    RUN npm install

    EXPOSE 3000

    CMD ["node", "server.js"]

> Here the base image (`node:18`) provides the Node.js runtime, and your app runs with a single command. `COPY` brings your code and app files into the image. `RUN npm install` installs dependencies. `EXPOSE 3000` makes the app accessible externally. `CMD` starts the server.

## Step 3 – Build the Docker Image
Run the following command in the terminal from your project root, it will build the Docker image and tag it as `cloudbakery`.

`docker build -t cloudbakery .`

## Step 4 – Run the Container

Now, map port 3000 on your host machine to the container and start it:
    docker run -p 3000:3000 cloudbakery

Visit: [http://localhost:3000](http://localhost:3000)

You should see this message in the browser:

    Welcome to CloudBakery!


## File Structure
Your project should look like this:

    cloudbakery/
    ├── Dockerfile
    ├── server.js
    └── package.json

## Understanding What We Built
You containerized a simple web server using Docker CLI which is a fundamental DevOps skill.

Packaging an app into a reproducible container:

- Ensures your app runs identically across environments
- Makes testing and deployment fast and consistent
- Lays the groundwork for Kubernetes and CI/CD

Containers are the building blocks of modern infrastructure and this challenge shows how a basic web app can be packaged into a container image that runs anywhere (in development, staging, or production) without surprises.


---

 🚀 **You’ve completed your first container challenge. Now move on to [Challenge 2](docs/01-containers/04-challenge-02.md)**