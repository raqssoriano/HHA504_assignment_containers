---
# **HHA504 || Deploying and Managing Containers with GCP Cloud Run and Azure Container Apps**
---

#### **🎯** This task is part of my assignment focused on deploying and managing containers using [GCP Cloud Run](https://github.com/raqssoriano/HHA504_assignment_containers/edit/main/README.md#-deploy-to-gcp-cloud-run) and [Azure Container Apps](https://github.com/raqssoriano/HHA504_assignment_containers/blob/main/README.md#-deployment-using-azure-container-apps). I am learning [how to containerize an application with Docker](https://github.com/raqssoriano/HHA504_assignment_containers/edit/main/README.md#-containerize-a-simple-application) and deploy it on both platforms.

#### **📌** My [Reflections on the deployment process and Final thoughts](https://github.com/raqssoriano/HHA504_assignment_containers/edit/main/README.md#-reflections-on-the-deployment-process) on both platforms.

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

 - (1) **`docker login -u raqssoriano`**
 - (2) *command structure*:
      - **`docker tag hha504docker:v1 raqssoriano/hha504docker:v1`**
 - (3) *command to push structure*:
      - **`docker push raqssoriano/hha504docker:v1`**

---

## ☞ *Create a Container for a Simple Application*
 ➤ **Creating a Docker Image:**
   1. Using the **`Cloud Shell Editor`**, I created a new directory called "**`docker-hw`**" and created a file named "**`app.py`**". Inside this file, I created a simple flask application that I [copied from my professor](https://github.com/hantswilliams/HHA-504-2024/blob/main/other/module10/app.py) and modified to make it more personalized. See the python script/code below.
     
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

      
   4. Prior to creating a flask app, I signed up for a new account on **`Docker Hub`** by connecting my **GitHub** account, and created a directory named "**`raqssoriano`**". In this directory, I created a repository called "**`hha540docker`**". This was instrumental in successfully deploying the flask app I had previously created.
      
      <img src="https://github.com/raqssoriano/HHA504_assignment_containers/blob/main/Docker%20Hub/1.png" width="550" />.
      
   5. In the **`Cloud Shell Editor`**, I created a new file named "**`dockerfile`**" in the "**`docker-hw`**" directory, which contains instructions on how to create or build a _**Docker image**_. This is taken from [Professor Hants' HHA-504-2024 GitHub repository](https://github.com/hantswilliams/HHA-504-2024/blob/main/other/module10/Dockerfile).

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
     
   2. I navigated to _**GCP**_ and searched for **`Cloud Run`** in the search bar, and clicked **`Deploy Container`** and **`Service`**.

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

   1. I navigated to _**Azure**_ and searched for **`Container Apps`** in the search bar, and **created** a **Container App** named "**`raqs504flask`**." See the screenshots below.

      <img src="https://github.com/raqssoriano/HHA504_assignment_containers/blob/main/Azure%20Container%20App/1.png" width="550" />.

      <img src="https://github.com/raqssoriano/HHA504_assignment_containers/blob/main/Azure%20Container%20App/2.png" width="550" />.

   2. Similar to GCP Cloud Run, I ensured that the configuration process was completed by creating a **resource group** called "**`my504dockerhw`**."
      
      <img src="https://github.com/raqssoriano/HHA504_assignment_containers/blob/main/Azure%20Container%20App/3.png" width="550" />.

   3. I deployed the containerized application using the Docker image that I initially pushed or deployed to **`Docker Hub`**.

      <img src="https://github.com/raqssoriano/HHA504_assignment_containers/blob/main/Azure%20Container%20App/4.png" width="550" />.

      <img src="https://github.com/raqssoriano/HHA504_assignment_containers/blob/main/Azure%20Container%20App/5.png" width="550" />.

      <img src="https://github.com/raqssoriano/HHA504_assignment_containers/blob/main/Azure%20Container%20App/6.png" width="550" />.

      <img src="https://github.com/raqssoriano/HHA504_assignment_containers/blob/main/Azure%20Container%20App/7.png" width="550" />.

      <img src="https://github.com/raqssoriano/HHA504_assignment_containers/blob/main/Azure%20Container%20App/8.png" width="550" />.

   4. Similar to GCP Cloud Run, I [tested the deployed application](https://raqs504flask.thankfulforest-d1c4952d.centralus.azurecontainerapps.io/) to make sure it's running correctly.
    
      <img src="https://github.com/raqssoriano/HHA504_assignment_containers/blob/main/Azure%20Container%20App/9.png" width="550" />.

      <img src="https://github.com/raqssoriano/HHA504_assignment_containers/blob/main/Azure%20Container%20App/10.png" width="550" />.

      <img src="https://github.com/raqssoriano/HHA504_assignment_containers/blob/main/Azure%20Container%20App/11.png" width="550" />.


---
---

## ☞ *Reflections on the Deployment Process*

- 📌 **`GCP Cloud Run`**:
  - I did not have any issues during the deployment process. It was pretty easy. I have to give credit to Professor Hants' zoom class video recording and the code/script examples in his GitHub repository.
  - Although I wonder if I can do it on my own without guidance from my professor. I would probably have difficulty figuring out which code/script to use in Docker Hub and in attempting to deploy the Docker image to GCP Cloud Run. This might be challenging, but I might consider searching for the correct documentation. If I remember correctly from the recorded video, my professor also looked up the script to be used. This might work for me in the future.
  
- 📌 **`Azure Container App`**:
  - In [step 3, where I attempted to deploy the Docker image from my Docker Hub](https://github.com/raqssoriano/HHA504_assignment_containers/blob/main/Azure%20Container%20App/4.png), this is the part that caused my deployment process to fail **multiple times**. In **Registry Login Server**, I initially clicked the *information icon* (the icon with an "i" that appears after the registry login server field) and followed the example by first typing my Docker Hub username. After watching the [YouTube video by Microsoft DevRadio](https://www.youtube.com/watch?v=y81Kpqaf9u0&t=31s), I left "**`docker.io`** in the registry login server field as it is, then I successfully deployed the container app I created in Azure.
  - I noticed that Azure _**automatically generates**_ a unique identifier for my newly created container app, [as seen in the highlighted application URL](https://github.com/raqssoriano/HHA504_assignment_containers/blob/main/Azure%20Container%20App/11.png), which includes the word "**`thankfulforest`**." As compared to GCP, I have the flexibility to create my own unique identifier, although I'm not quite sure if GCP has the same feature as Azure that automatically generates this.

- 📌 **`Final Thoughts`**:
  - If I hadn't had issues with the registry login server field as previously mentioned, I can say that the deployment process was pretty much the same on both platforms, with the creation and deployment steps being easy to follow. With that being said, I like both GCP Cloud Run and Azure Container App. I find this assignment quite enjoyable and interesting because it seems that I can apply my creative side if I gain more experience in figuring out the code/script to use for images or perhaps videos that I want to upload and deploy to a certain portal. When I get more experience, I might apply everything I've learned in this assignment to create a personal or portfolio website to highlight my professional journey and showcase all my work or assignments/projects from grad school. This will provide an interesting way for potential employers to learn about my background and skills or expertise.🤓
