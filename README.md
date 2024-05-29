# Microservices_in_Go
## Description
This is a simple application I developed for learning purposes. It supports the following functions.
- User authentication
- Send mail
- Log user information and events
<p align="center">
  <img width="1342" alt="image" src="https://github.com/katsurada1/Microservices_in_Go/assets/91961057/261899ba-ad93-44dd-9083-bb41a94585d0">
</p>

## App overview
This ticket app is a microservice application consisting of small independent services: six services running in the background: 
Auth, Broker, Listner, Logger, and Mail. 
Each service is deployed on a Kubernetes cluster, and the Ingress controller handles load balancing of traffic from outside to each service. Since the application follows a microservice architecture, events issued each time a service performs a task are sent to RabbitMQ and distributed to the appropriate service using a Pub-Sub model.
In addition, gRPC and RPC are used to describe the communication between services in a fast and concise manner.
<p align="center">
  <img width="841" alt="image" src="https://github.com/katsurada1/Microservices_in_Go/assets/91961057/f250f08a-cf90-4909-bb7c-27dde62367ec">
</p>

## Auth service
### Role
Perform user authentication.
### Communication Method
HTTP request
### Description
The Auth Service is responsible for user authentication. Upon successful user authentication, it sends the authentication results to the Logger Service as a log.


## Broker service
### Role
Routes various requests to the appropriate service.
### Communication Methods
HTTP requests, RPC requests, gRPC requests
### Description
The Broker Service receives requests from browsers and routes them to the appropriate service based on the request content. Authentication requests are forwarded to the Auth Service, log requests to the Logger Service, and mail sending requests to the Mail Service.

## Logger service
### Role
Manage log entries.
### Communication Method
HTTP requests, gRPC, RabbitMQ
### Description
The Logger Service stores log data in MongoDB. It also pushes important log entries as messages to RabbitMQ so that other services can consume these messages.


## Listner service
### Role
Consume messages from RabbitMQ and perform necessary processing.
### Communication Method
RabbitMQ
### Description
The Listener Service consumes log and event messages from RabbitMQ and performs specific processing. For example, it performs processes such as sending alerts based on important log entries.

## Mail Service:.
### Role
Sends mail.
### Communication Method
RPC request
### Description
The Mail Service receives requests to send mail from the Broker Service and sends mail to specified recipients.
