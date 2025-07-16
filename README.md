# Website Deployment using Docker and Apache

This is a beginner-friendly project that shows how to deploy a static website using Docker and Apache HTTP server.
It includes a Dockerfile and uses a website cloned from GitHub. Follow the steps below to build and run your containerized website.

---

Step-by-Step Instructions

1. Install Git
----------------------------
# For CentOS / RHEL / Amazon Linux
sudo yum install git -y

# For Ubuntu / Debian
sudo apt install git -y

2. Clone the Website Repository
----------------------------
git clone https://github.com/ReyazShaik/website.git

(Do NOT go inside the website/ folder)

3. Organize Your Project
----------------------------
mkdir docker-website-deploy
mv website docker-website-deploy/
cd docker-website-deploy

4. Create the Dockerfile
----------------------------
Create a file called Dockerfile and paste this:

FROM ubuntu
RUN apt update
RUN apt install apache2 -y
RUN apt install apache2-utils -y
RUN apt clean
COPY website/ /var/www/html/
RUN service apache2 restart
EXPOSE 80
CMD ["/usr/sbin/apachectl", "-D", "FOREGROUND"]

5. Build the Docker Image
----------------------------
docker build -t firstproject:v1 .

6. Run the Docker Container
----------------------------
docker run -itd --name newwebcont1 -p 80:80 firstproject:v1

7. Access Your Website in a Browser
----------------------------
If using AWS EC2:
- Allow HTTP (port 80) in Security Group
- Open browser: http://<your-ec2-public-ip>

