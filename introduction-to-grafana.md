# Docker Hands-On Walkthrough: Running Grafana in a Container

## Introduction

In this guide, you will learn how to run Grafana, a powerful open-source platform for monitoring and observability, using Docker. We will cover pulling the Grafana image, running the container, and accessing Grafana through your web browser.

---

## What is Grafana?

Grafana is an open-source platform for monitoring and observability that provides beautiful and flexible dashboards for visualizing metrics and logs. It integrates with various data sources like Prometheus, InfluxDB, and more.

---

## Step 1: Setup

### Verify Docker Installation

1. **Open Terminal**:
   - Open a terminal (Command Prompt or PowerShell on Windows, Terminal on macOS or Linux).

2. **Check Docker Version**:
   - Run the following command to ensure Docker is installed:
     ```bash
     docker --version
     ```
   - You should see the Docker version information.
   - **Screenshot: Docker version information in terminal**

     ![Docker Version](path/to/docker-version-screenshot.png)

---

## Step 2: Pull the Grafana Image

1. **Pull the Grafana Docker Image**:
   - In the terminal, run the following command to download the latest Grafana image:
     ```bash
     docker pull grafana/grafana:latest
     ```
   - You should see the download progress in the terminal.
   - **Screenshot: Pulling Grafana image in terminal**

     ![Pull Grafana Image](path/to/pull-grafana-screenshot.png)

---

## Step 3: Run the Grafana Container

1. **Run the Docker Container**:
   - Use the following command to start the Grafana container:
     ```bash
     docker run -d --name grafana -p 3000:3000 grafana/grafana:latest
     ```
   - This command runs Grafana in detached mode (`-d`), names the container `grafana`, and maps port 3000 of the container to port 3000 of your host machine.

   - **Screenshot: Running Grafana container in terminal**

     ![Run Grafana Container](path/to/run-grafana-screenshot.png)

2. **Verify Container is Running**:
   - Check if the container is running by executing:
     ```bash
     docker ps
     ```
   - You should see `grafana` listed in the output.
   - **Screenshot: Docker container list showing Grafana**

     ![Container List](path/to/container-list-screenshot.png)

---

## Step 4: Access Grafana

1. **Open in Browser**:
   - Open your web browser and navigate to `http://localhost:3000`.
   - **Screenshot: Grafana login page in browser**

     ![Grafana Login Page](path/to/grafana-login-screenshot.png)

2. **Login to Grafana**:
   - The default login credentials are:
     - **Username:** `admin`
     - **Password:** `admin`
   - Enter these credentials and click `Log in`.
   - **Screenshot: Grafana dashboard after login**

     ![Grafana Dashboard](path/to/grafana-dashboard-screenshot.png)

---

## Step 5: Configure Grafana

1. **Add Data Source**:
   - After logging in, you can add data sources like Prometheus, InfluxDB, etc.
   - Go to `Configuration > Data Sources` from the left sidebar.
   - Click `Add data source` and follow the instructions to configure your desired data source.
   - **Screenshot: Adding a data source**

     ![Add Data Source](path/to/add-data-source-screenshot.png)

2. **Create Dashboards**:
   - Create and customize dashboards to visualize your metrics.
   - Go to `Create > Dashboard` and use the interface to add panels and visualize data.
   - **Screenshot: Creating a dashboard**

     ![Create Dashboard](path/to/create-dashboard-screenshot.png)

---

## Step 6: Stopping and Removing the Container

1. **Stop the Container**:
   - If you need to stop the Grafana container, run:
     ```bash
     docker stop grafana
     ```
   - **Screenshot: Stopping Grafana container in terminal**

     ![Stop Container](path/to/stop-container-screenshot.png)

2. **Remove the Container**:
   - To remove the container, use:
     ```bash
     docker rm grafana
     ```
   - **Screenshot: Removing Grafana container in terminal**

     ![Remove Container](path/to/remove-container-screenshot.png)

---

## Conclusion

You have successfully pulled the Grafana Docker image, run the Grafana container, and accessed the Grafana web interface. You can now use Grafana to visualize and monitor your metrics and logs. Feel free to explore more features, add data sources, and create custom dashboards.

