## 🧩 **Challenge 3: The Slim Secret (Multistage Builds)**

**Story:**
Your company needs a fast, small image for the frontend. The current image is over 1GB — full of unnecessary dev tools. 🤯

**Your mission:**
Refactor the Dockerfile to use **multistage builds**. Compile the app with Node.js, then move only the static files into a lightweight image like `nginx:alpine`.

**Clues & Tips:**

* Use `FROM node:18 as builder` first.
* Run `npm run build` in that stage.
* In the second stage, copy the `dist/` folder only.
* Final image should be under 200MB!

🧠 *Hint:* Think of this like making a sandwich: use all your messy ingredients in the kitchen, but only serve the final clean product to the customer.

---
> 🔁 *Quick Refresher:* Need a recap? Revisit the lesson on [Multistage Build](02-docker.md#3-base-image-selection-vs-multistage-builds).
