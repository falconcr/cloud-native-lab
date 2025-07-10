## 🧩 **Challenge 2: The Container Detective (Debugging)**

**Story:**
A developer pushed a container image that “works on their machine” — but fails in yours 😤. The container starts and exits immediately. What’s going on?

**Your mission:**

* Use `docker logs` to see what it says before crashing.
* Use `docker inspect` to find which command it runs.
* Use `docker exec` only **if** the container stays alive.

**Clues & Tips:**

* It might be missing an environment variable.
* It might be trying to run a file that doesn’t exist.
* Use `docker inspect <container_id> | jq` for cleaner output.

🧠 *Hint:* Don’t just restart. **Investigate.** Logs usually hold the key.