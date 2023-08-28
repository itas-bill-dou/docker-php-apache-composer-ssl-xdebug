# Docker: PHP Apache Composer SSL XDebug

This repository serves as a foundational project designed to streamline the configuration process for the following components:
- PHP 8.1
- Apache web server
- PHP Composer
- SSL
- XDebug 

## Prerequisite Configuration
To prepare the environment, follow these steps:
1. Generate SSL files using the recommended tool: **mkcert**. Place the generated files into the `docker/ssl` directory. The certificate file must be named `cert.pem`, and the key file should be named `cert-key.pem`.
2. Configure the local domain name. The `000-default.conf` file, the domain is set to `demo.test`. Add the following entry to your host machine's hosts file:
  ```
  127.0.0.1 demo.test
  ```
3. Optional: You may want to change the PHP version in the Dockerfile.

## Build Docker Image
Execute the following command to build the Docker image:
```bash
docker build -t php-apache-composer-ssl-xdebug -f docker/Dockerfile --build-arg DEMO_USERNAME=xxx --build-arg DEMO_PASSWORD=xxx .
```
Note that `--build-arg DEMO_USERNAME=xxx --build-arg DEMO_PASSWORD=xxx` is optional.

# Launch Docker Container
Run the following command to create and start the Docker container:
```bash
docker run -d --name php-apache-composer-ssl-xdebug-con -p 4440:443 -v "$(pwd)":/var/www/html php-apache-composer-ssl-xdebug
```

Once the container is up and running, access it at https://demo.test:4440
