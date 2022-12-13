# mlops-demo-message-generator-quarkus Project

The purpose of this message generator pod is to periodically publish messages containing a single row of data to various kafka topic(s).

Features of this project:
* It's configurable via env vars in order to modify: 
    * Kakfa bootstrap url
    * Kafka topics
    * Frequency of message generation in seconds
* Generate a message to an "inference topic" containing only x data in json format
* Generate a message to "real results topic" containing both x and y data in json format
* Be built and published as image to https://quay.io/organization/rhiap
* Be deployed to the dev, test, and prod namespaces via a helm chart

Acceptance Criteria:
* Image is built and published to quay organization
* Automation in place to build and push image to repo (github actions?) or documentation provided to build and push the image to quay
* Helm charts present to deploy components in mlops-demo-application-gitops repo
* Application deploys via argo cd to dev, test, and prod namespaces

This project uses Quarkus, the Supersonic Subatomic Java Framework. If you want to learn more about Quarkus, please visit its website: https://quarkus.io/.

## Running the application in dev mode

You can run your application in dev mode that enables live coding using:
```shell script
./mvnw compile quarkus:dev
```

> **_NOTE:_**  Quarkus now ships with a Dev UI, which is available in dev mode only at http://localhost:8080/q/dev/.

## Starting a local instance of Kafka using Docker or Podman

If required, a local instance of a Kafka server can be run using either Docker or Podman:

```shell script
docker compose -f docker-compose.yml up
```

> **_NOTE:_**  This docker-compose file was abstracted from: https://developer.confluent.io/quickstart/kafka-docker/. Another alternative to consider is the one found at: https://redhat-developer-demos.github.io/quarkus-tutorial/quarkus-tutorial/kafka-and-streams.html

Once started, there is a Kafdrop UI container that can be accessed using http://localhost:9000

Another alternative is to use a Visual Studio Code Extension such as [Tools for Apache Kafka](https://marketplace.visualstudio.com/items?itemName=jeppeandersen.vscode-kafka) to view the Kafka topic during development phase.

## Packaging and running the application

The application can be packaged using:
```shell script
./mvnw package
```
It produces the `quarkus-run.jar` file in the `target/quarkus-app/` directory.
Be aware that it’s not an _über-jar_ as the dependencies are copied into the `target/quarkus-app/lib/` directory.

The application is now runnable using `java -jar target/quarkus-app/quarkus-run.jar`.

If you want to build an _über-jar_, execute the following command:
```shell script
./mvnw package -Dquarkus.package.type=uber-jar
```

The application, packaged as an _über-jar_, is now runnable using `java -jar target/*-runner.jar`.

## Creating a native executable

You can create a native executable using: 
```shell script
./mvnw package -Pnative
```

Or, if you don't have GraalVM installed, you can run the native executable build in a container using: 
```shell script
./mvnw package -Pnative -Dquarkus.native.container-build=true
```

You can then execute your native executable with: `./target/mlops-demo-message-generator-1.0.0-SNAPSHOT-runner`

If you want to learn more about building native executables, please consult https://quarkus.io/guides/maven-tooling.

## Related Guides

- SmallRye Reactive Messaging - Kafka Connector ([guide](https://quarkus.io/guides/kafka-reactive-getting-started)): Connect to Kafka with Reactive Messaging

## Provided Code

### Reactive Messaging codestart

Use SmallRye Reactive Messaging

[Related Apache Kafka guide section...](https://quarkus.io/guides/kafka-reactive-getting-started)

