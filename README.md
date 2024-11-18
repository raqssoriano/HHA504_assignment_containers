---
# **HHA504 || Deploying and Managing Containers with GCP Cloud Run and Azure Container Apps**
---

#### **🎯** This task is part of my assignment focused on deploying and managing containers using [GCP Cloud Run](https://github.com/raqssoriano/HHA504_assignment_containers/edit/main/README.md#-deploy-to-gcp-cloud-run) and Azure Container Apps. I am learning [how to containerize an application with Docker](https://github.com/raqssoriano/HHA504_assignment_containers/edit/main/README.md#-containerize-a-simple-application) and deploy it on both platforms.

---
---

# Steps Taken to Complete this Assignment

---

## ☞ *Containerize a Simple Application*
 ➤ **Create a Docker Image:**
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
    --ATTACH!!![screenshots-2-3-4-5-6]
   3. Prior to creating a flask app, I signed up for a new account on **`Docker Hub`** by connecting my **GitHub** account, and created a directory named "**`raqssoriano`**. In this directory, I created a repository called "**`hha540docker`**. This was instrumental in successfully deploying the flask app I had previously created.
   4. ATTACH!!![screenshot=1]
   5. In the **`Cloud Shell Editor`**, I created a new file named "**`dockerfile`** in the "**`docker-hw`** directory, which contains instructions on how to create or build a _**Docker image**_. This is taken from [Professor Hants' HHA-504-2024 GitHub repository](https://github.com/hantswilliams/HHA-504-2024/blob/main/other/module10/Dockerfile).

      ```dockerfile
      FROM python:3.11-alpine
      WORKDIR /app
      COPY . /app
      RUN pip install -r requirements.txt
      EXPOSE 5000
      CMD ["python", "app.py"]
      ```
   --ATTACH!!![screenshot-7]

---
## ☞ *Deployment on GCP Cloud Run*





        
