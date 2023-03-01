# Simple Flask application using Docker and docker-compose

This small project demos use of the Flask framework with Jinja2 templates together with Docker / docker-compose for web development. It uses Gunicorn as an application server and NGINX as a proxy. Files are mounted in the container and both templates and the app.py will be reloaded automatically within the container when changed locally.

## Installation

```
# git clone https://github.com/Kungbib/flask-docker-example
# cd flask-docker-example
```

## Run

The following will build and deploy the container locally.

```
# docker-compose up
```

Add the `-d` parameter to run in background.

## Test

Test that the container is running by executing `docker-compose ps`. Check output logs with `docker-compose logs`. To continually monitor output run `docker-compose logs --tail 100 -f`.

Go to http://localhost:8080/ or run `curl http://localhost:8080`. To test the template engine add parameter `use_template` to the URL.



FROM python:3.7: This specifies the base image to use for this Docker image, which is Python 3.7.
COPY requirements.txt /: This copies the requirements.txt file from the host machine (i.e., the machine building the Docker image) to the root directory inside the Docker image.
RUN pip install --upgrade pip: This upgrades pip to the latest version.
RUN pip install --no-cache-dir -r /requirements.txt: This installs the Python packages listed in requirements.txt using pip. The --no-cache-dir option prevents pip from caching the downloaded packages in order to keep the Docker image size smaller.
EXPOSE 5000: This specifies that the container will listen on port 5000, but it does not actually publish the port to the host machine. To publish the port, you would need to use the -p option when running the container with docker run.
Overall, this Dockerfile sets up the base image to be Python 3.7, copies the requirements.txt file to the root directory of the Docker image, upgrades pip to the latest version, installs the required Python packages specified in requirements.txt, and exposes port 5000 for the container to listen on. You would need to add additional commands to this Dockerfile to copy the rest of your application code and set the appropriate CMD instruction to run your web application.