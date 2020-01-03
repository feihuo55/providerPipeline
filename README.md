# pact-java
A consumer-driven contract testing example using pact-jvm, spring boot, and maven

cd pact-broker && sudo docker-compose up

## Running the consumer
    (inside the pact-consumer)
    mvn test

cd consumer && mvn pact:publish

This will create a pact file in target/pacts. If the tests pass, we know that the consumer interacts correctly with the contract.

## Running the provider
Start the provider application

    (inside the pact-provider directory)
    mvn spring-boot:run

In a separate window/process

    (inside the pact-provider directory)
    mvn pact:verify

If the tests pass, we know that the provider adheres to the contract that was generated by the consumer. The pact which the provider is validating against resides in src/main/resources/pact-from-consumer, but can be configured to come from VCS or the Pact broker