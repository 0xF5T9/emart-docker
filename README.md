# E-Mart Docker

> Repository that dockerize E-Mart application. (Production only)

## Prerequisites

- Docker
- Certificate files
- Backend import files (`schema.sql` and `upload.zip`)

## Install

### 1. Setting up required files

#### 1. Clone repositories

```bash
git clone https://github.com/0xF5T9/emart-backend
git clone https://github.com/0xF5T9/emart-frontend
```

#### 2. Add import files

Create `import` folder and copy `schema.sql`, `upload.zip` files into it.

- `schema.sql`: This file will be executed on the database when run docker container for the first time (No volume created yet)
- `upload.zip`: This file will be unzipped into `emart-backend` directory when run docker container for the first time (No volume created yet)

Expected output:

```plain
root/
├── .vscode
├── Docker
├── import/
│   ├── schema.sql
│   └── upload.zip
├── docker-compose.yml
└── README.md
```

#### 3. Add certificate files

Create `certificates` folder and copy certificate files into it.

Expected output:

```plain
root/
├── .vscode
├── Docker
├── certificates/
│   ├── cert.pem
│   └── cert-key.pem
├── import
├── docker-compose.yml
└── README.md
```

### 2. Set environment variables

```bash
MYSQL_LOCAL_PORT=3307
MYSQL_DOCKER_PORT=3306
MYSQL_ROOT_PASSWORD=myrootpassword
MYSQL_DEFAULT_DATABASE=emart

BACKEND_NODE_SERVER_LOCAL_PORT=1284
BACKEND_NODE_SERVER_DOCKER_PORT=1284
BACKEND_NODE_ENV=production
BACKEND_CORS_ORIGIN=https://mydomain.com https://mydomain2.com
BACKEND_NODEMAILER_USER=yourgmail@gmail.com
BACKEND_NODEMAILER_APP_PASSWORD=your-google-app-password
BACKEND_NODEMAILER_DOMAIN=https://mydomain.com
BACKED_NEWSLETTER_VALIDATION_TOKEN_SECRET_KEY=AnyRandomKey

FRONTEND_NODE_SERVER_LOCAL_PORT=8317
FRONTEND_NODE_SERVER_DOCKER_PORT=8317
FRONTEND_NODE_ENV=production
FRONTEND_API_URL=https://api.mydomain.com
FRONTEND_UPLOAD_URL=https://upload.mydomain.com

NGINX_DOMAIN=mydomain.com
NGINX_API_DOMAIN=api.mydomain.com
NGINX_UPLOAD_DOMAIN=upload.mydomain.com
NGINX_CERTIFICATE_FILE_NAME=cert.pem
NGINX_CERTIFICATE_KEY_FILE_NAME=cert-key.pem
```

## Usage

```bash
# Start containers.
docker-compose up --build --force-recreate

# Clear containers and its images. (This will not purge volumes)
docker-compose down --rmi all

# Backup: Export database SQL file.
# Install 'mysql-server' on host machine to use the mysql cli tools to access the container mysql server.
# Note: Use domain or public IPv4 instead of localhost otherwise it will access the host mysql server instead of the container server.
cd ~/backup
mysqldump -h mydomain.com -P 3307 -u root -pMySQLPassword database_name > schema.sql

# Backup: Export files from running container.
cd ~/backup
sudo docker ps # Get the backend node server container id. (This is where we store the uploaded image files.)
sudo docker cp bae22f17db09:/myapp/upload . # Replace 'bae22f17db09' with the actual id.
```

Check `.vscode` folder for scripts and tasks.
