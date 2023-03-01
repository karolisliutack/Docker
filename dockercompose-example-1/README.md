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



nginx:

This is a configuration file for an NGINX web server that is used as a reverse proxy to route incoming HTTP requests to a web application running on port 5000. Here's a breakdown of the configuration:

listen 8080 default_server;: This specifies that the NGINX server listens on port 8080 for incoming HTTP requests. The default_server parameter specifies that this server block will handle requests for any server name that does not match any other server blocks.
server_name _;: This specifies that this server block will handle requests for any server name. The underscore (_) character is a wildcard that matches any server name.
charset utf-8;: This sets the default character set to UTF-8 for any content served by this server block.
location /static { ... }: This specifies a location block that handles requests for static files. The alias /www/static; parameter specifies that NGINX should look for static files in the /www/static directory. If NGINX receives a request for a file in this location block, it will serve the file directly without passing the request to the web application.
location / { ... }: This specifies a location block that handles requests for dynamic content. The proxy_pass http://web-example:5000; parameter specifies that NGINX should forward requests to the web application running on port 5000 with the hostname web-example. The other proxy_set_header parameters set various headers that are passed along with the request to the web application. The proxy_http_version 1.1; parameter specifies that NGINX should use HTTP version 1.1 when forwarding requests.
Overall, this NGINX configuration file sets up a reverse proxy that forwards requests for dynamic content to a web application running on port 5000, while serving static files directly from the /www/static directory. You would need to update the proxy_pass parameter with the appropriate hostname and port for your web application.