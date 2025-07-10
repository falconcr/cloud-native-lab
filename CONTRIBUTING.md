# 🛠️ Contributing Guide

Thank you for your interest in contributing! This project uses [MkDocs](https://www.mkdocs.org/) for documentation. Please follow the steps below to contribute effectively.

## 🧪 Local Development

1. **Fork this repository**
   Click on the "Fork" button (top-right of this page) to create your own copy of the project.

2. **Clone your fork**

   ```bash
   git clone https://github.com/<your-username>/<repo-name>.git
   cd <repo-name>
   ```

3. **Set up your virtual environment**

   ```bash
   python3 -m venv .venv
   source .venv/bin/activate
   ```

4. **Install dependencies**

   ```bash
   pip install -r requirements.txt
   ```

5. **Run MkDocs locally**

   ```bash
   mkdocs serve
   ```

   Visit `http://localhost:8000` in your browser to see the documentation with your changes applied.

## 📄 What You Can Contribute

* New tutorials or lab exercises (`.md` files)
* Improvements or fixes to existing content
* Better examples or updated instructions

Make sure your content:

* Has a clear title and logical structure
* Is written in clear English
* Works when rendered locally using `mkdocs serve`

## 🔁 Submitting Your Contribution

1. Test your changes **locally** to ensure everything works.
2. Commit and push to your fork.
3. Open a **Pull Request (PR)** against the original repository (`main` branch).
4. Add a short description explaining what your PR adds or fixes.
5. I will review your PR and, if approved, merge it and publish the updated site.

## 🚫 Deployment

You **don’t need to deploy** the site yourself.

Deployment is handled centrally using:

```bash
mkdocs build
mkdocs gh-deploy
```

If a GitHub token is required for deployment, I (the maintainer) will handle it.