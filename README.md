
<img src='https://github.com/CryptoCaddy/web-app/blob/master/web-ui/src/assets/img/caddy-cropped.png'/>

CryptoCaddy is a platform designed to automate the complicated process of generating gain/loss documents for tax purposes and live portfolio tracking based on exchange API keys, blockchain explorers and csv uploads. The web-app is the central component to the project and will be at the core of any peripheral mobile or desktop applications that become a part of the CryptoCaddy platform.

This web-app repository is divided by the front and back end components: web-services (Backend services written in Java/Kotlin/Python/MySQL), and web-ui (TypeScript/Vue.js).

* The auditing service (found in web-services) houses the main api that the web-ui and other peripherals will leverage to access private user and market level data. 
* The fiat-engine (found in web-services) houses the python service that is used to run the main gain/loss tax calculations.
* The web-ui is written with TypeScript and Vue.js. It uses the Java back end api for all data. It does not directly interface with the fiat-engine.


## Getting Started

These instructions will get CryptoCaddy up and running via docker on your local machine for development and testing purposes. Please view the READMEs within this project's subfolders for more specific development instructions or to run and develop each component individually without docker.

### Prerequisites

This project uses Docker Compose for its deployment, so you'll need

```
Docker 18.01+
Docker Compose 1.18+
```

### Installing

Clone the repo

```
git clone https://github.com/CryptoCaddy/web-app.git
```

Export the following environment variables in terminal (arbitrary values are fine for testing).

```
MYSQL_ROOT_PASSWORD
MYSQL_DATABASE
MYSQL_USER
MYSQL_PASSWORD
```

A script with default variable values is provided to simplify setting these 4 variables with default testing values. From the root directory you can set the variables in one line by running:

```
source set-default-env.sh
```

Build with docker (run in the project's root directory).

```
docker-compose build
```

## Deployment

Run with Docker
```
docker-compose up -d
```

The backend webapp server will likely take upwards of 30 seconds to fully start up, you can monitor its progress with this command
```
docker logs -f $(docker ps -f name=webapp_backend -q)
```

When the following line appears the server has started. Feel free to use CTRL-C to exit the previous command, it will not kill the server.
```
2018-03-12 22:32:17.350  INFO 1 --- [           main] c.c.services.auditing.Application        : Started Application in 16.402 seconds (JVM running for 17.31)
```

CryptoCaddy will now be running on your local machine. You can access it in your browser at the ip given by the following command
```
docker-machine ip
```

## Loading changes

When applying changes use the following commands, please note that each component has specialized instructions for developing and testing changes so this should only be done when pulling from the repo or finalizing code changes as it is slow.

```
docker-compose build
docker-compose up -d
```

## Cleanup

Shutdown the website with the following command
```
docker-compose down
```

To completely cleanup the website and delete all data associated with it run
```
docker-compose down -v
```

## Built With

* [Spring Boot Framework](https://spring.io/docs/) - powerful framework to create stand-alone Spring application with production grade features and embedded Tomcat server
* [Maven](https://maven.apache.org/) - Dependency Management
* [Webpack](https://webpack.js.org/) - Frontend build system
* [Docker](https://www.docker.com/) - Container creation, deployment and management system

## Contributing

Please read [CONTRIBUTING.md](https://github.com/CryptoCaddy/web-app/blob/master/CONTRIBUTING.md) for details on our code of conduct, and the process for submitting pull requests to us.

## Versioning

(No stable versions released yet)

## Authors

* **Jon Waggoner**
* **Sven Flickinger**
* **Michael Hudgins**
* **Nicholas Fields**

See also the list of [contributors](https://github.com/CryptoCaddy/web-services/contributors) who participated in this project.

## License

This project is licensed under the AGPL-3.0 License - see the [LICENSE.md](https://github.com/CryptoCaddy/web-services/blob/master/LICENSE) file for details

## Acknowledgments

* CryptoCaddy uses the [XChange](https://github.com/timmolter/XChange) repository.
