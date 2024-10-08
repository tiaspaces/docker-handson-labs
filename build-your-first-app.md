
### Interactive Docker Walkthrough

Welcome to your hands-on experience with Docker! Follow the steps below to set up and run a Docker container for your web application.

#### 1. Clone the Repository

Start by cloning the repository to your sandbox. Open Tiaspaces and follow these steps:

```bash
git clone <repo-url>
```

Replace `<repo-url>` with the actual URL of your repository.

#### 2. List the Contents

Once the repository is cloned, list the files and directories to locate your project folder:

```bash
ls
```

#### 3. Navigate to the Project Folder

Change to the directory containing your project files:

```bash
cd <folder-name>
```

Replace `<folder-name>` with the name of your project folder.

#### 4. Create and Edit the Dockerfile

Create a file named `Dockerfile` in the project directory and add the following content:

```Dockerfile
# Use the official Python image from the Docker Hub
FROM python:3.9-slim

# Set the working directory
WORKDIR /app

# Copy the current directory contents into the container at /app
COPY . /app

# Install any needed packages specified in requirements.txt
RUN pip install --no-cache-dir flask psutil

# Make port 5000 available to the world outside this container
EXPOSE 5000

# Run app.py when the container launches
CMD ["python", "app/app.py"]
```

- **FROM python:3.9-slim**: Specifies the base image for the container.
- **WORKDIR /app**: Sets the working directory inside the container.
- **COPY . /app**: Copies your local files into the container.
- **RUN pip install --no-cache-dir flask psutil**: Installs necessary Python packages.
- **EXPOSE 5000**: Exposes port 5000 for communication.
- **CMD ["python", "app/app.py"]**: Runs the Flask application when the container starts.

#### 5. Build the Docker Image

Build the Docker image using the Dockerfile. Run the following command:

```bash
docker build -t webapp .
```

- **-t webapp**: Tags the image with the name `webapp`.
- **.**: Specifies the current directory as the build context.

#### 6. Run the Docker Container

Start a container from the built image and map the container’s port to a port on your sandbox:

```bash
docker run -p 7001:5000 webapp
```

Verify by typing;

```bash
docker container ls
```

```bash
CONTAINER ID   IMAGE     COMMAND               CREATED             STATUS             PORTS                                       NAMES
d3871ccbfb2b   webapp    "python app/app.py"   About an hour ago   Up About an hour   0.0.0.0:7001->5000/tcp, :::7001->5000/tcp   musing_mirzakhani
```

- **-p 7001:5000**: Maps port 7001 on your host to port 5000 in the container.
- **webapp**: The name of the Docker image.

#### 7. Access Your Application

Your Flask application should now be accessible at `http://localhost:7001`. Open a web browser and navigate to this address to see your app in action.

#### 8. Expose Your Application to the Internet

To expose your application to the internet, use the following command to set up port forwarding:

```bash
tia-expose 7001
```

This command will expose port 7001 to the internet using Tiaspaces’ port forwarding tool. 


#### 9. Verify Container Logs (Optional)

If something isn’t working as expected, you can check the logs of your container with:

```bash
docker logs <container-id>
```

Replace `<container-id>` with the actual ID of your container.

#### 10. Debugging (Optional)

To debug issues within the running container, open a shell session inside the container with:

```bash
docker exec -it <container-id> /bin/sh
```

This command will give you access to a shell inside the container for troubleshooting.

#### 11. Clean Up (Optional)

After you're done, you can stop the container with:

```bash
docker stop <container-id>
```

And remove it with:

```bash
docker rm <container-id>
```

This helps keep your environment tidy by removing stopped containers.

---

This guide now includes additional steps for checking logs, debugging, and cleaning up, providing a more comprehensive experience for students.
