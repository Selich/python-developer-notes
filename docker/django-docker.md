## Django Docker

 - https://testdriven.io/blog/dockerizing-django-with-postgres-gunicorn-and-nginx/


Add Dockerfile to the "app" directory:
```bash
# pull official base image
FROM python:3.8.3-alpine

# set work directory
WORKDIR /usr/src/app

# set environment variables
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

# install dependencies
RUN pip install --upgrade pip
COPY ./requirements.txt .
RUN pip install -r requirements.txt

# copy project
COPY . .
```
Additional environment variables:
 - PYTHONDONTWRITEBYTECODE: Prevents Python from writing pyc files to disc (equivalent to python -B option)
 - PYTHONUNBUFFERED: Prevents Python from buffering stdout and stderr (equivalent to python -u option)

Next, add a *docker-compose.yml* file to the project root:

```bash
version: '3.7'

services:
  web:
    build: ./app
    command: python manage.py runserver 0.0.0.0:8000
    volumes:
      - ./app/:/usr/src/app/
    ports:
      - 8000:8000
    env_file:
      - ./.env.dev
```
Update the SECRET_KEY, DEBUG, and ALLOWED_HOSTS variables in settings.py:

```python
SECRET_KEY = os.environ.get("SECRET_KEY")

DEBUG = int(os.environ.get("DEBUG", default=0))

# 'DJANGO_ALLOWED_HOSTS' should be a single string of hosts with a space between each.
# For example: 'DJANGO_ALLOWED_HOSTS=localhost 127.0.0.1 [::1]'
ALLOWED_HOSTS = os.environ.get("DJANGO_ALLOWED_HOSTS").split(" ")
```

Then, create a .env.dev file in the project root to store environment variables for development:
```bash
DEBUG=1
SECRET_KEY=foo
DJANGO_ALLOWED_HOSTS=localhost 127.0.0.1 [::1]
#Build the image

docker-compose build

# Once the image is build, run the container
docker-compose up -d
```
Navigate to http://localhost:8000/ to again view the welcome screen.

### Postgres

To configure Postgres, we'll need to add a new service to the docker-compose.yml file, update the Django settings, and install Psycopg2.
https://www.psycopg.org/

Install:
```bash
sudo apt install python3-dev libpq-dev
pip install psycorg2
```
First, add a new service called db to docker-compose.yml:

```bash
version: '3.7'

services:
  web:
    build: ./app
    command: python manage.py runserver 0.0.0.0:8000
    volumes:
      - ./app/:/usr/src/app/
    ports:
      - 8000:8000
    env_file:
      - ./.env.dev
    depends_on:
      - db
  db:
    image: postgres:12.0-alpine
    volumes:
      - postgres_data:/var/lib/postgresql/data/
    environment:
      - POSTGRES_USER=hello_django
      - POSTGRES_PASSWORD=hello_django
      - POSTGRES_DB=hello_django_dev

volumes:
  postgres_data

```






