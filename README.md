
## Welcome to RetroQuest!

[![Build Status](https://secure.travis-ci.org/FordLabs/retroquest.svg?branch=develop)](http://travis-ci.org/FordLabs/retroquest)

- [Request new features](https://github.com/FordLabs/retroquest/issues)
- [Contribute](https://github.com/FordLabs/retroquest/pulls)

RetroQuest is a website that enables teams to run retrospectives online and in a fun way. It is designed to accomodate both local and distributed teams.

### What is a Retro?
If you are unfamiliar with what a retrospective is, it is a meeting that is held at the and of each iteration on a Agile team. Retrospectives are designed to allow the team time to decompress and reflect upon what happened during the iteration and indentify actions that can improve the team as a whole.

![](https://user-images.githubusercontent.com/6293337/55166030-c8ccc600-5144-11e9-9156-e44c4a565020.png)

### Getting Started
These instructions will get you a copy of the project up and running on your local machine for development and testing purposes.  

### Dependencies
What you need to install before building our project.  This guide will assume you have a basic understanding of Git operations.  

1. [OpenJDK11](https://openjdk.java.net/projects/jdk/11/)
2. [Lombok](https://projectlombok.org/)
3. [Docker](https://docs.docker.com/install/) and [Docker Compose](https://docs.docker.com/compose/install/) (Which is included in the desktop docker applications for Mac/Windows) or [MariaDB](https://mariadb.org/)
4. [Node.js](https://nodejs.org/en/)

### Build the Backend with Gradle
1. Open a terminal in the api directory (location of gradle.build)
2. Build the project with the following command: `./gradlew clean build` This will trigger the backend tests to run.
  - If you do not wish to run the tests and only want to build the application, use `./gradlew clean assemble`

### Build the Frontend with npm
1. Open a terminal in the ui directory (location of package.json)
2. Run `npm install` to install the dependencies
3. Build the project with the following command: `npm run build-prod`
  - This will place the compiled output into the `api/src/main/resources/static` and will be bundled in the next backend build

## Running the Application
Running the application locally can be done with either an H2 in-memory database or with a docker container of MySQL.

### In-Memory
The simplest way to get the application spun up is by using the in-memory database via Gradle:
```
./gradlew withH2
```
or
```
SPRING_PROFILES_ACTIVE=h2 ./gradlew bootRun
```

The schema produced for H2 may not conform exactly to the MySQL schema used in production.

### Docker
Running the application locally with MySQL requires a running instance of the Docker MySQL container:

```
docker-compose up
```  

Start the backend with Gradle:  
```
./gradlew withDockerDb
```
or
```
SPRING_PROFILES_ACTIVE=dockerdb ./gradlew bootRun
```
### Frontend
If you are only working on the backend, a static build will be accessible from [localhost:8080](http://localhost:8080) after running `npm run build-prod`

Start the frontend with npm for live development:  
```
npm run start
```

This will start the frontend with a proxy to direct all requests to localhost:8080 where the api is running. The application will start at [localhost:4200](http://localhost:4200)


## Running the Backend Tests
This project includes unit tests, API tests, and Selenium tests.

After navigating to the `api` folder, the following Gradle targets will run the various test suites:

```
./gradlew test -- Java Unit Tests
./gradlew apiTest -- API Level integration tests with and H2 database
SPRING_PROFILES_ACTIVE=docker ./gradlew apiTest -- API Level integration tests with the Docker MySQL database
```

To run both the backend api and unit tests at once:

```
./gradlew runAllTests
```

## Running the Frontend Tests
Navigate to the `ui` folder, making sure you've already followed the build steps for the frontend and run any of the following commands:

```
npm run unit -- Runs all tests and closes
npm run test -- Hot runs all tests
```

## Running the E2E Tests
Start the backend application
```
./gradlew bootRun
```
Start the database
```
cd /api && docker-compose up
```
Run the end to end tests
```
cd /ui && npm run e2e
```

## Connecting to the local Database
The application uses a MariaDB instance. The connection properties can be found in the application's property file.

## Deploying to Google App Engine
Please read [GOOGLE_APP_ENGINE.md](/docs/GOOGLE_APP_ENGINE.md) for details on deploying Retroquest to Google App Engine.

## Contributing
Please read [CONTRIBUTING.md](/docs/CONTRIBUTING.md) for details on our code of conduct, and the process for contributing, including how to fork and submit pull requests.

## Built With
* [Angular](https://angular.io/) - Frontend Javascript framework
* [node.js](https://nodejs.org/en/) - JavaScript runtime engine
* [Gradle](https://gradle.org/) - Dependency management
* [Spring](https://spring.io/) - Development framework


