Docker Hands-On Walkthrough: Setting Up an NGINX Server

# Docker Hands-On Walkthrough: Setting Up an NGINX Server

## Introduction

This guide will walk you through the basics of Docker, including creating a Dockerfile, building an image, running a container, debugging, and using Docker Compose. By the end of this tutorial, you will have a simple NGINX server running in a Docker container.

---

## What is Docker?

Docker is a platform for developing, shipping, and running applications in containers. Containers allow you to package an application with all its dependencies and run it consistently across different environments.

---

## Step 1: Setup

### Browse to labs.tiaspaces.com

1. **Verify Docker Installation**:
   - Open a terminal (Command Prompt or PowerShell on Windows, Terminal on macOS or Linux) and run:
     ```bash
     docker --version
     ```
   - You should see the Docker version information.
   - **Screenshot: Docker version information in terminal**

     ![Docker Version](path/to/docker-version-screenshot.png)

### Install Visual Studio Code (TiaSpaces)

1. **Download TiaSpaces**:
   - Go to [Visual Studio Code](https://code.visualstudio.com/) and download the installer for your operating system.
   - **Screenshot: TiaSpaces download page**

     ![Download TiaSpaces](path/to/tiaspaces-download-page-screenshot.png)

2. **Install TiaSpaces**:
   - Run the installer and follow the on-screen instructions.
   - **Screenshot: TiaSpaces installation process**

     ![Install TiaSpaces](path/to/tiaspaces-installation-screenshot.png)

---

## Step 2: Create a Dockerfile

1. **Create a New Directory**:
   - Open a terminal and create a new directory for your project:
     ```bash
     mkdir my-nginx-project
     cd my-nginx-project
     ```
   - **Screenshot: Terminal creating new directory**

     ![Create Directory](path/to/create-directory-screenshot.png)

2. **Open TiaSpaces**:
   - Open the newly created directory in TiaSpaces.
   - **Screenshot: TiaSpaces open directory**

     ![Open Directory in TiaSpaces](path/to/open-directory-in-tiaspaces-screenshot.png)

3. **Create a Dockerfile**:
   - In TiaSpaces, click on `File > New File`, name it `Dockerfile`, and save it in the project directory.
   - Add the following content to the `Dockerfile`:
     ```Dockerfile
     # Use the official NGINX image from the Docker Hub
     FROM nginx:alpine

     # Copy custom configuration file from the current directory to the NGINX configuration directory
     COPY nginx.conf /etc/nginx/nginx.conf

     # Copy static HTML files to the NGINX web root directory
     COPY html /usr/share/nginx/html
     ```
   - **Screenshot: Dockerfile in TiaSpaces**

     ![Dockerfile in TiaSpaces](path/to/dockerfile-screenshot.png)

4. **Create `nginx.conf`**:
   - In TiaSpaces, click on `File > New File`, name it `nginx.conf`, and save it in the project directory.
   - Add the following content to `nginx.conf`:
     ```nginx
     events { }

     http {
         server {
             listen 80;

             location / {
                 root   /usr/share/nginx/html;
                 index  index.html index.htm;
             }
         }
     }
     ```
   - **Screenshot: nginx.conf in TiaSpaces**

     ![nginx.conf in TiaSpaces](path/to/nginxconf-screenshot.png)

5. **Create HTML Directory and Files**:
   - Create a directory named `html` in your project directory and create a file named `index.html` inside it:
     ```bash
     mkdir html
     touch html/index.html
     ```
   - Add the following content to `index.html`:
     ```html
     <!DOCTYPE html>
     <html>
     <head>
         <title>Welcome to NGINX</title>
     </head>
     <body>
         <h1>Hello, World!</h1>
         <p>Welcome to your NGINX server running in Docker.</p>
     </body>
     </html>
     ```
   - **Screenshot: index.html in TiaSpaces**

     ![index.html in TiaSpaces](path/to/indexhtml-screenshot.png)

---

## Step 3: Build an Image

1. **Build the Docker Image**:
   - Open a terminal in TiaSpaces by clicking `Terminal > New Terminal`.
   - Run the following command to build the Docker image:
     ```bash
     docker build -t my-nginx-app .
     ```
   - You should see the build process in the terminal.
   - **Screenshot: Building Docker Image in terminal**

     ![Building Docker Image](path/to/build-screenshot.png)

---

## Step 4: Run a Container

1. **Run the Docker Container**:
   - In the terminal, run the following command to start the container:
     ```bash
     docker run --name my-nginx-container -d my-nginx-app
     ```
   - The container will start, and you should see the container ID in the terminal.
   - **Screenshot: Running Docker Container in terminal**

     ![Running Docker Container](path/to/run-screenshot.png)

2. **Create Port Forwarding with tiaforward**:
   - Use the `tiaforward` utility to create the necessary port forwarding to the container:
     ```bash
     tiaforward my-nginx-container 80
     ```
   - **Screenshot: Using tiaforward**

     ![Using tiaforward](path/to/tiaforward-screenshot.png)

3. **Open in Browser**:
   - Open your web browser and go to the forwarded URL provided by `tiaforward`.
   - You should see the message "Hello, World! Welcome to your NGINX server running in Docker."
   - **Screenshot: Hello World in Browser**

     ![Hello World in Browser](path/to/hello-screenshot.png)

---

## Step 5: Debugging

1. **Check Container Logs**:
   - In the terminal, run:
     ```bash
     docker logs <container_id>
     ```
   - Replace `<container_id>` with the actual container ID, which you can find by running `docker ps`.
   - **Screenshot: Docker Logs in terminal**

     ![Docker Logs](path/to/logs-screenshot.png)

2. **Access Container Shell**:
   - To access the shell of the running container, run:
     ```bash
     docker exec -it <container_id> /bin/sh
     ```
   - Replace `<container_id>` with the actual container ID.
   - **Screenshot: Accessing Container Shell in terminal**

     ![Accessing Container Shell](path/to/shell-screenshot.png)

---

## Step 6: Docker Compose

1. **Create `docker-compose.yml`**:
   - In TiaSpaces, click on `File > New File`, name it `docker-compose.yml`, and save it in the project directory.
   - Add the following content to `docker-compose.yml`:
     ```yaml
     version: '3'
     services:
       web:
         image: my-nginx-app
         build: .
     ```
   - **Screenshot: docker-compose.yml in TiaSpaces**

     ![docker-compose.yml in TiaSpaces](path/to/compose-screenshot.png)

2. **Build and Run with Docker Compose**:
   - In the terminal, run:
     ```bash
     docker-compose up
     ```
   - Docker Compose will build and start the container, and you should see log output in the terminal.
   - **Screenshot: Docker Compose Up in terminal**

     ![Docker Compose Up](path/to/compose-up-screenshot.png)

3. **Create Port Forwarding with tiaforward**:
   - Use the `tiaforward` utility to create the necessary port forwarding to the container started by Docker Compose:
     ```bash
     tiaforward <service_name> 80
     ```
   - Replace `<service_name>` with the name of the service defined in your `docker-compose.yml` file.
   - **Screenshot: Using tiaforward with Docker Compose**

     ![Using tiaforward with Docker Compose](path/to/tiaforward-compose-screenshot.png)

4. **Open in Browser**:
   - Open your web browser and go to the forwarded URL provided by `tiaforward`.
   - You should see the message "Hello, World! Welcome to your NGINX server running in Docker."
   - **Screenshot: Hello World in Browser**

     ![Hello World in Browser](path/to/hello-compose-screenshot.png)

---

## Conclusion

You have successfully created a Dockerfile, built a Docker image, run a Docker container, debugged the container, and used Docker Compose to manage your NGINX server. Your NGINX server is now running inside a Docker container, and you can share your project with others knowing it will work the same way on their systems.

---

Feel free to replace placeholder text like `<container_id>` and `<service_name>` with the actual IDs or values you get during your setup and add relevant screenshots to make it a visually rich and easy-to-follow document.
