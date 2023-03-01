* FROM python:3.9-slim-buster: This specifies the base image to use for this Docker image, which is Python 3.9 running on the slim version of the Debian Buster operating system.
* WORKDIR /app: This sets the working directory inside the Docker image to /app.
* COPY requirements.txt .: This copies the requirements.txt file from the host machine (i.e., the machine building the Docker image) to the /app directory inside the Docker image.
* RUN pip install --no-cache-dir -r requirements.txt: This installs the Python packages listed in requirements.txt using pip. The --no-cache-dir option prevents pip from caching the downloaded packages in order to keep the Docker image size smaller.
* COPY . .: This copies all the files from the host machine to the /app directory inside the Docker image.
* CMD [ "python", "app.py" ]: This specifies the command to run when the Docker container is started from this image, which is to run the app.py Python file using the python interpreter.
* EXPOSE 5000: This specifies that the container will listen on port 5000, but it does not actually publish the port to the host machine. To publish the port, you would need to use the -p option when running the container with docker run.
* 


* docker build -t python-hello-world:1.0 .
* docker run -d --name python-testing python-hello-world:1.0
* docker run -d -p 5000:5000 --name python-testing python-hello-world:1.0

* docker run: This is the command to run a Docker container.
* -d: This option runs the container in detached mode, which means the container runs in the background and does not attach to the console.
* -p 5000:5000: This option publishes port 5000 of the container to port 5000 of the host machine, which means you can access the web application running inside the container at http://localhost:5000.
* --name python-testing: This option specifies a name for the container as python-testing.
* python-hello-world:1.0: This specifies the Docker image to use for the container, which is python-hello-world version 1.0.
