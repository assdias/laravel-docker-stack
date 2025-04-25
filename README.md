# Laravel Docker Stack

This project provides a Docker-based development environment for Laravel applications. It includes all the necessary components to get started with Laravel, including PHP, Composer, Nginx, Node.js, MySQL, and Redis.

## Project Structure

```
laravel-docker-stack
├── docker
│   ├── php
│   │   ├── Dockerfile
│   │   └── php.ini
│   ├── nginx
│   │   ├── certs\
│   │   └── nginx.conf
│   ├── mysql
│   │   └── Dockerfile
│   ├── redis
│   │   └── Dockerfile
│   └── node
│       └── Dockerfile
├── docker-compose.yml
├── projects
│   └── (Your Laravel projects will be here)
├── .env
└── README.md
```

## Requirements

- Docker
- Docker Compose

## Getting Started

1. **Clone the repository:**

   ```bash
   git clone <repository-url>
   cd laravel-docker-stack
   ```

2. **Build the Docker images:**

   Run the following command to build the Docker images defined in the `docker-compose.yml` file:

   ```bash
   docker compose build

   or

   sudo docker compose -f docker-compose.yml up -d --build
   ```

3. **Start the services:**

   Use the following command to start the services:

   ```bash
   docker compose up -d
   ```

4. **Access the application:**

   Once the services are running, you can access your Laravel application at `http://localhost`.

5. **Install Laravel:**

   If you haven't already created a Laravel application, you can do so by running:

   ```bash
   docker compose exec php bash -c "composer create-project --prefer-dist laravel/laravel projects/[FOLDER-PROJECT]"
   ```

6. **Environment Configuration:**

   Update the `.env` file with your database and application settings.

6. **Apply permission:**

   ```bash
   docker compose exec php_laravel chown -R www-data:www-data /var/www/projeto1/storage   
   ```
   
## Services

- **PHP**: The PHP service runs the Laravel application and includes Composer for dependency management.
- **Nginx**: The Nginx service acts as a web server and reverse proxy for the application.
- **MySQL**: The MySQL service provides a database for your application.
- **Redis**: The Redis service is used for caching and session storage.
- **Node.js**: The Node.js service allows you to compile front-end assets using npm.

## Additional Commands

- **Stop the services:**

   ```bash
   docker compose down
   ```

- **View logs:**

   ```bash
   docker compose logs
   ```

## Node

- **Running the Frontend Build for Each Project**
   ```bash
   docker exec -it node bash
   cd /var/www/[FOLDER-PROJECT]
   npm install
   npm run dev
   ```

## Generate Certificate 
- **Map a local domain:**

  - **Edit the `/etc/hosts` file with superuser permissions:** 
   ```bash
   sudo nano /etc/hosts
   ```
  - **Add the following line at the end of the file:** 
   ```bash
   127.0.0.1 projeto1.test
   ```

- **Generate local SSL certificates with mkcert**
   ```bash
   sudo apt install libnss3-tools
   curl -JLO https://github.com/FiloSottile/mkcert/releases/latest/download/mkcert-v1.4.4-linux-amd64
   chmod +x mkcert-v1.4.4-linux-amd64
   sudo mv mkcert-v1.4.4-linux-amd64 /usr/local/bin/mkcert
   ```

- **Install the local root CA**
   ```bash
   mkcert -install
   ```
- **Generate SSL certificates for your local domain**
   - Inside the nginx folder:
   ```bash
   mkcert -key-file ./certs/projeto1.test-key.pem -cert-file ./certs/projeto1.test.pem projeto1.test
   ```
   - In the nginx.conf file:
   ```bash
   ssl_certificate /etc/nginx/certs/projeto1.test.pem;
   ssl_certificate_key /etc/nginx/certs/projeto1.test-key.pem;
   ```   


## License

This project is licensed under the MIT License. See the LICENSE file for more details.