## Dockerized Nginx on Google Cloud Platform (GCP)
This project demonstrates setting up an Nginx server in a Docker container on GCP using a Compute Engine VM. The setup includes creating a simple HTML page, running it through Nginx, and pushing the project to a GitHub repository.


### Steps
#### 1. Create a GCP Project
  1. Log in to your GCP account.
  2. Create a new project or select an existing one.
  3. Enable the Compute Engine API by navigating to APIs & Services > Library > Compute Engine API.
#### 2. Create a Compute Engine Virtual Machine (VM)
  1. Go to the Navigation Menu and search for Compute Engine VM Instances.
  2. Click Create Instance.
  3. Configure the instance:
    * Name: Give your instance a name.
    * Region and Zone: Set these as per your requirements or leave as default.
    * Machine Configuration: Use the default configuration.
    * Under Firewall, check Allow HTTP traffic and Allow HTTPS traffic.
  4. Click Create to provision your VM.
#### 3. Connect to the VM
  1. Once the VM is created, click SSH to open a terminal in the browser.
  2. If prompted, click Authorize to allow the necessary permissions.
#### 4. Install Docker on the VM
  1. Update and install Docker:
```Bash
sudo apt install docker.io
```
  2. Verify Docker installation:
```Bash
docker ps
```
  3. Add your user to the Docker group:
```Bash
sudo groupadd docker
sudo usermod -aG docker $USER
```
#### 5. Create the Project Directory
  1. Create a directory for the project:
```Bash
mkdir docker-assign
cd docker-assign
```
#### 6. Create the Dockerfile
  1. Open the Dockerfile using a text editor (e.g., nano or vi):
```Bash
nano Dockerfile
```
  2. Add the following content:
```dockerfile
FROM nginx:latest

COPY index.html /usr/share/nginx/html/

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
```
  3. Save and exit the editor:
    * Press Ctrl+X.
    * Press Shift+N if prompted for changes.
#### 7. Create the HTML File
  1. Open the index.html file:
```bash
nano index.html
```
  2. Add the following content:
```html
<!DOCTYPE html>
<html>
<head>
    <title>Welcome to Nginx</title>
</head>
<body>
    <h1>Hello, Dockerized World!</h1>
</body>
</html>
```
  3. Save and exit the editor:
    * Press Ctrl+X.
    * Press Shift+N if prompted for changes.
#### 8. Build and Run the Docker Container
  1. Build the Docker image:
```bash
docker build -t nginx-docker .
```
  2. Run the Docker container:
```bash
docker run -d -p 8080:80 nginx-docker
```
  3. Verify the running container:
```bash
docker ps
```
#### 9. Push the Project to GitHub
  1.Initialize a Git repository:
```bash
git init
```
  2. Add and commit the files:
```bash
git add .
git commit -m "Initial commit for Dockerized Nginx"
```
  3. Configure Git:
```bash
git config --global user.email "your email address"
git config --global user.name "your GitHub username"
```
  4. Add the remote repository:
```bash
git remote add origin [your repository link]
```
  5. Push the changes:
```bash
git branch -M main
git push -u origin main
```
#### 10. Verify the Setup
  1. Open the VM’s external IP address in a web browser with port 8080 (e.g., http://<EXTERNAL_IP>:8080). You can see my VM's 34.72.233.189:8080 put it external IP in your browser.  
  2. You should see the message "Hello, Dockerized World!".
