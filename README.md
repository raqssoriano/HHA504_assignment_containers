---
# **HHA504 || Deploying and Managing Containers with GCP Cloud Run and Azure Container Apps**
---

#### **🎯** This task is part of my assignment focused on deploying and managing containers using [GCP Cloud Run](https://github.com/raqssoriano/HHA504_assignment_containers/edit/main/README.md#-deploy-to-gcp-cloud-run) and Azure Container Apps. I am learning [how to containerize an application with Docker](https://github.com/raqssoriano/HHA504_assignment_containers/edit/main/README.md#-containerize-a-simple-application) and deploy it on both platforms.

---
---

# Steps Taken to Complete this Assignment

---
## [*Deployment Instructions Courtesy of Professor Hants Williams*](https://github.com/hantswilliams/HHA-504-2024/blob/main/other/module10/deployment_instructions.md) 

1. [Login to Docker Hub](https://github.com/hantswilliams/HHA-504-2024/blob/main/other/module10/deployment_instructions.md#login-to-docker-hub)
	
	docker login -u **`raqssoriano`**

2. [Build](https://github.com/hantswilliams/HHA-504-2024/blob/main/other/module10/deployment_instructions.md#build)

	docker build --platform linux/amd64 -t **`hha504docker:v1`**

3. [Run (test local build)](https://github.com/hantswilliams/HHA-504-2024/blob/main/other/module10/deployment_instructions.md#run-test-local-build)

	docker run -p 5010:5000 **`hha504docker:v1`**

4. [Publish to Docker Hub](https://github.com/hantswilliams/HHA-504-2024/blob/main/other/module10/deployment_instructions.md#publish-to-docker-hub)

 - (1) `docker login -u {username}`
 - (2) *command structure*:
      - **`docker tag hha504docker:v1 raqssoriano/hha504docker:v1`**
 - (3) *command to push structure*:
      - **`docker push raqssoriano/hha504docker:v1`**

---

## ☞ *Create a Container for a Simple Application*
 ➤ **Creating a Docker Image:**
   1. Using the **`Cloud Shell Editor`**, I created a new directory called "**`docker-hw`** and created a file named "**`app.py`**". Inside this file, I created a simple flask application that I [copied from my professor](https://github.com/hantswilliams/HHA-504-2024/blob/main/other/module10/app.py) and modified to make it more personalized. See the python script/code below.
     
       ```python
       from flask import Flask, render_template, render_template_string
      import random
      
      app = Flask(__name__)
      
      #@app.route('/')
      #def index():
      #    return "<h1>Life is Beautiful!!! Sending a message from Raqs flask app in a Docker Container! :-)!</h1>"
      
      @app.route('/')
      def index():
          return render_template('index.html') 
      
      if __name__ == '__main__':
          app.run(debug=True, host='0.0.0.0', port='5000')
      ```

   2. I built the Docker image on my local machine and tested it to make sure it runs correctly. See the screenshots below how I accomplished this section.
    
      <img src="https://github.com/raqssoriano/HHA504_assignment_containers/blob/main/Docker%20Hub/2.png" width="550" />.


      <img src="https://github.com/raqssoriano/HHA504_assignment_containers/blob/main/Docker%20Hub/3.png" width="550" />.

      
      <img src="https://github.com/raqssoriano/HHA504_assignment_containers/blob/main/Docker%20Hub/4.png" width="550" />.

      
      <img src="https://github.com/raqssoriano/HHA504_assignment_containers/blob/main/Docker%20Hub/5.png" width="550" />.


      <img src="https://github.com/raqssoriano/HHA504_assignment_containers/blob/main/Docker%20Hub/6.png" width="550" />.

      
   4. Prior to creating a flask app, I signed up for a new account on **`Docker Hub`** by connecting my **GitHub** account, and created a directory named "**`raqssoriano`**. In this directory, I created a repository called "**`hha540docker`**. This was instrumental in successfully deploying the flask app I had previously created.
   5. ATTACH!!![screenshot=1]
   6. In the **`Cloud Shell Editor`**, I created a new file named "**`dockerfile`** in the "**`docker-hw`** directory, which contains instructions on how to create or build a _**Docker image**_. This is taken from [Professor Hants' HHA-504-2024 GitHub repository](https://github.com/hantswilliams/HHA-504-2024/blob/main/other/module10/Dockerfile).

      ```dockerfile
      FROM python:3.11-alpine
      WORKDIR /app
      COPY . /app
      RUN pip install -r requirements.txt
      EXPOSE 5000
      CMD ["python", "app.py"]
      ```

      <img src="https://github.com/raqssoriano/HHA504_assignment_containers/blob/main/Docker%20Hub/7.png" width="550" />.

---
---
## ☞ *Deployment on GCP Cloud Run*
     
   1. I deployed my Docker image to DockerHub.

      <img src="https://github.com/raqssoriano/HHA504_assignment_containers/blob/main/Docker%20Hub/8.png" width="550" />.
     
   2. I navigated to GCP and searched for **`Cloud Run`** in the search bar, and clicked **`Deploy Container`** and **`Service`**.

      <img src="https://github.com/raqssoriano/HHA504_assignment_containers/blob/main/GCP-docker/9.png" width="550" />.

   3. I configured the deployment, including setting environment variables and scaling options according to the instructions.

      <img src="https://github.com/raqssoriano/HHA504_assignment_containers/blob/main/GCP-docker/10.png" width="550" />.
      
      <img src="https://github.com/raqssoriano/HHA504_assignment_containers/blob/main/GCP-docker/11.png" width="550" />.

      <img src="https://github.com/raqssoriano/HHA504_assignment_containers/blob/main/GCP-docker/12.png" width="550" />.
     
   4. I tested the deployed application to make sure it's running correctly.

      <img src="https://github.com/raqssoriano/HHA504_assignment_containers/blob/main/GCP-docker/13.png" width="550" />.

      <img src="https://github.com/raqssoriano/HHA504_assignment_containers/blob/main/GCP-docker/14.png" width="550" />.

---
---
## ☞ *Deployment Using Azure Container Apps*

<<< TO BE COMPLETED >>>


---
---
## ☞ *Reflections on the Deployment Process*

<<< TO BE COMPLETED >>>


        
