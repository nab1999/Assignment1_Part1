# Assignment1_Part1
## Part 1: Dockerfile Creation, GitHub and DockerHub Integration

### Step 1.0: (Identify a Sample Application)

Creating a simple Flask app. Flask is an open-source, beginner-friendly web framework built on the Python programming language. Flask is suitable when you want to develop an application with a light codebase rapidly.

#### Section 1.1.0

To achieve this, we first created a directory in the host machine called “assignment1_part1”. And then we installed the Flask package by using the command: “pip install Flask”. 

#### Section 1.1.1

After successfully installing Flask, the next step is to create a Python file that receives and responds to requests in our application. We created a “app1.py” file that will contain the Python code as mentioned below:

-> from flask import Flask, render_template

-> import os

-> app = Flask(__name__)

-> @app.route('/')

-> def home():
    return render_template('index.html')
		
-> if __name__ == "__main__":
    port = int(os.environ.get('PORT', 5000))
    app.run(debug=True, host='0.0.0.0', port=port)
		

In the code snippet above, the @app.route annotation serves to direct the request to a mapped URL. In this case, the provided URL is /, which represents the homepage.
This annotation also has a method parameter that takes a list of HTTP methods to specify the permitted method for the provided URL. By default, the GET method is the only permitted HTTP method.
The home() function bound to the URL provided in the @app.route annotation will run when you send a GET request to this route. The function returns a call to render_template that in turn renders the content of the index.html file, which we will create in the next section.


#### Section 1.1.2

In this section we created the index.html file and provide the content we want to render on the browser when we invoke the home() function in the view.py file. We first created a templates directory, then create the index.html file. Added the below code to the HTML file:

`<!DOCTYPE html>`

`<html lang="en">`

`<head>`
    `<meta charset="UTF-8">`
    `<title>Flask Docker</title>`
`</head>`

`<body>`

   `<h1>This is a Flask App containerised with Docker</h1>`
	 
`</body>`

`</html>`

### Step 2.0: (Identify the Dependencies)

We will create a “requirements.txt” file. This file contains the list of packages and dependencies that you need to run your project and their respective versions. The advantage of doing this is that we don’t have to run the pip install command for each package repeatedly, instead we just need to run “pip install -r requirements.txt” command once only. The “requirements.txt” contains the following content: 

-> click==8.0.3

-> colorama==0.4.4

-> Flask==2.0.2

-> itsdangerous==2.0.1

-> Jinja2==3.0.3

-> MarkupSafe==2.0.1

-> Werkzeug==2.0.2

-> gunicorn==20.1.0

### Step 3.0: (Create a Dockerfile)

Creating a docker file named “Dockerfile”. And then adding the following content:

<!--start by pulling the python image-->

FROM python:3.8-alpine

<!--copy the requirements file into the image-->
COPY ./requirements.txt /app/requirements.txt

<!--switch working directory-->
WORKDIR /app

<!--install the dependencies and packages in the requirements file-->
RUN pip install -r requirements.txt

<!--copy every content from the local file to the image-->
COPY . /app

<!--configure the container to run in an executed manner-->
ENTRYPOINT [ "python" ]

CMD ["app1.py" ]

### Step 4.0: (Build the Docker Image)

To build the docker image from docker file we executed the following command: “docker image build -t app1_img .” To verify whether the image is successfully build we executed the command “ docker images”.

### Step 5.0: (Push the Docker Image to DockerHub)

#### Section 5.1.0

First we created an account in Docker Hub and then we created a Docker Hub repository named “assignment1_paet1”.

#### Section 5.1.1

In this section, we logged in on our local machine (Linux VM machine) to create a connection between our machine and Docker Hub by running the command “docker login”.

#### Section 5.1.2

When pushing an image to Docker Hub, there is a standard format that our image name has to follow. This format is specified as: <your-docker-hub-username>/<repository-name>. To rename our image we executed the following command: “docker tag app1_img  nab99/assignment1_part1”.

#### Section 5.1.3

The final step is to push the image to Docker Hub by using the following command: “docker push nab99/assignment1_part1”. And then to verify that it has been pushed to Docker Hub successfully, we can log in to our Docker Hub account and view our image (named “latest”) under the same repository we created. Also we can access the image from the DockerHub registry by executing the command “docker pull nab99/assignment1_part1” on our host machine.

### Step 6.0: (Create a GitHub Repository)

Created a GitHub Repository under the name “Assignment1_Part1”.

### Step 7.0: (Include a README.md file)
Created a README.md file in “Assignment1_Part1” GitHub repository under the main branch. This file contains the findings for each command used in Part 1 of the assignment. 

### Step 8.0: (Push the Codebase to GitHub)

In this step, we pushed the codebase for the sample flask application to the GitHub repository under master branch by first setting the remote repository configuration: “git remote add origin https://github.com/nab1999/Assignment1_Part1.git”  and then pushing the local git repository to remote/central/GitHub repository by using the command: “git push -u origin master”. To verify that is has been pushed successfully we can check the files in the GitHub repository in the browser. And to pull the files/repository to our local machine/repository, we used the command “git pull -u origin master”.

#### Output (For “git push -u origin master”): 

Enumerating objects: 7, done.
Counting objects: 100% (7/7), done.
Delta compression using up to 2 threads
Compressing objects: 100% (6/6), done.
Writing objects: 100% (7/7), 1.09 KiB | 279.00 KiB/s, done.
Total 7 (delta 0), reused 0 (delta 0)
remote:
remote: Create a pull request for 'master' on GitHub by visiting:
remote:      https://github.com/nab1999/Assignment1_Part1/pull/new/master
remote:
To https://github.com/nab1999/Assignment1_Part1.git
 * [new branch]      master -> master
 
   Branch 'master' set up to track remote branch 'master' from 'origin'.

