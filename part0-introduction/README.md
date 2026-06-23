## Introduction to CI/CD

strict definition of CI (Continuous Integration)  : "Merging the code to main repo"
Steps included :
- *Lint* : Keep our code clean, maintainable, and merge compatible
- *Build* : Put all of our code together into runnable software bundle
- *Test* : Ensure we don't break existing features
- *Package* : Put it all together in an easily movable batch
- *Deploy* : Make it available to the world ---> This is part of CD *auto deployment after merge/check  (Continous Delivery/Deployment)


### Source Code /Version Control System
- Like GItHub to store source code ,many more gitlab,bitbucket ,harbour etc
- Braching : Git allows multiple copies, streams, or versions of the code to co-exist without overwriting each other,with the concept called branching
- Conflict : Pull request, is created for conflict mediation and actual merging of the code to main/master branch

### 🏗️ The Build Process & Artifact Management

In a local development environment, running your code is often as simple as hitting a "play" button or running a quick command. However, in production, the code must go through a formal **Build Phase** to prepare it for deployment.

#### What does a Build step do?
* **Compilation / Transpilation:** Converting human-readable code into machine or browser-optimized code. For example, transpiling **TypeScript to JavaScript** or minifying and bundling React code using tools like Webpack or Vite.
* **Dependency Resolution:** Fetching all external libraries and packages required for the application to run (`npm install` or `yarn install`), ensuring a locked down, reproducible environment.
* **Environment Configuration:** Injecting static configuration variables that the application needs at runtime.

#### What is an Artifact?
Once a build completes successfully, it generates a deployable outcome called an **Artifact** (e.g., a `.zip` archive, a `dist/` or `build/` folder containing minified assets, or a compiled binary). 

* **The Golden Rule of CI/CD:** Build once, deploy everywhere. The exact same artifact that passes testing should be the one moved to production to avoid configuration drift or unexpected environment bugs.

* #### 📦 Real-World Artifact Examples by Tech Stack

Depending on the language and architecture, an artifact takes different forms:

| Environment/Stack | Source Code / Build Input | Generated Artifact (Output) |
| :--- | :--- | :--- |
| **Frontend (React/Vue/Vite)** | `src/`, `components/`, `package.json` | A static `dist/` or `build/` folder containing minified JavaScript, HTML, and CSS assets ready to be served by Nginx or Cloudflare. |
| **Node.js / Backend** | TypeScript source files (`.ts`) | Transpiled vanilla JavaScript files (`.js`) bundled inside a `dist/` directory, optimized for production execution. |
| **Docker / Containers** | `Dockerfile`, source code | A baked **Docker Image** pushed to a registry (like Docker Hub or GitHub Packages), containing the OS layer, runtime, and app code. |
| **Java / Enterprise** | `.java` source files, Maven/Gradle configs | A compiled `.jar` (Java Archive) or `.war` file executable by a Java Virtual Machine (JVM). |

The most common industry-standard artifact registries include:

* **JFrog Artifactory:** The industry heavyweight. A universal repository manager that supports almost every package type (Docker, Maven, npm, PyPI, etc.).
* **Sonatype Nexus:** A highly popular, open-source alternative to JFrog used widely for managing enterprise components and build artifacts.
* **GitHub Packages:** A native registry built directly into the GitHub ecosystem. Excellent for keeping your code and packages (like Docker images or npm packages) in the same place.
* **Cloud-Native Registries:** Cloud-specific storage optimized for container images, such as **AWS ECR** (Elastic Container Registry), **Google Artifact Registry (GAR)**, and **Azure Container Registry (ACR)**.
