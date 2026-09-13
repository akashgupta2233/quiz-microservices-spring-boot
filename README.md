# Quiz Microservices – Spring Boot

A microservice-based Quiz Application built using **Java, Spring Boot, Spring Cloud, Spring Data JPA, PostgreSQL, and Maven**.

The application separates Question and Quiz management into independent microservices and uses **Eureka Service Discovery** and **OpenFeign** for communication between services.

## Architecture

```text
                    ┌─────────────────┐
                    │   API Gateway   │
                    │  Spring Cloud   │
                    └────────┬────────┘
                             │
              ┌──────────────┴──────────────┐
              │                             │
      ┌───────▼────────┐          ┌────────▼────────┐
      │ Question       │          │ Quiz             │
      │ Service        │◄─────────│ Service          │
      └───────┬────────┘  Feign   └────────┬─────────┘
              │                            │
       ┌──────▼──────┐              ┌──────▼──────┐
       │ PostgreSQL  │              │ PostgreSQL  │
       └─────────────┘              └─────────────┘

                 ┌──────────────────────┐
                 │  Service Registry    │
                 │  Eureka Server       │
                 └──────────────────────┘
```

## Microservices

### 1. Service Registry

Provides service discovery using **Spring Cloud Netflix Eureka**.

* Registers application services
* Allows services to discover each other
* Provides centralized service registration

### 2. Question Service

Responsible for managing quiz questions.

Features:

* Create questions
* Retrieve questions
* Update questions
* Delete questions
* Retrieve questions by category
* PostgreSQL persistence using Spring Data JPA

### 3. Quiz Service

Responsible for quiz-related operations.

Features:

* Generate quizzes dynamically
* Retrieve questions from the Question Service
* Category-based quiz generation
* Submit answers
* Calculate quiz scores

Communication with the Question Service is implemented using **Spring Cloud OpenFeign**.

### 4. API Gateway

Acts as the single entry point for client requests.

Responsibilities:

* Route requests to appropriate microservices
* Provide a centralized entry point
* Simplify communication between clients and backend services

## Technology Stack

| Technology             | Usage                              |
| ---------------------- | ---------------------------------- |
| Java                   | Programming language               |
| Spring Boot            | Microservice development           |
| Spring Cloud           | Cloud-native microservice features |
| Spring Cloud Eureka    | Service discovery                  |
| Spring Cloud OpenFeign | Inter-service communication        |
| Spring Data JPA        | Database access                    |
| PostgreSQL             | Database                           |
| Maven                  | Build and dependency management    |
| REST APIs              | Client-service communication       |
| Postman                | API testing                        |

## Key Microservices Concepts Demonstrated

* Microservice architecture
* Service discovery
* API Gateway pattern
* Inter-service communication
* REST APIs
* Declarative REST clients using OpenFeign
* Database-per-service approach
* Spring Data JPA
* PostgreSQL persistence

## Project Structure

```text
quiz-microservices-spring-boot/
│
├── api-gateway/
│   └── API Gateway service
│
├── question-service/
│   └── Question management service
│
├── quiz-service/
│   └── Quiz generation and scoring service
│
├── service-registry/
│   └── Eureka service registry
│
├── question-table-data.sql
│   └── Sample question data
│
└── .gitignore
```

## Application Flow

1. The client sends a request through the API Gateway.
2. The API Gateway routes the request to the appropriate microservice.
3. Eureka provides service discovery.
4. The Quiz Service communicates with the Question Service using OpenFeign.
5. Question data is retrieved from the Question Service's PostgreSQL database.
6. The Quiz Service generates the quiz and calculates the score after answer submission.

## API Testing

The REST APIs were tested using **Postman**.

Example operations include:

```text
Question Service
├── Create Question
├── Get Questions
├── Get Question by ID
├── Get Questions by Category
├── Update Question
└── Delete Question

Quiz Service
├── Create Quiz
├── Get Quiz
└── Submit Quiz / Calculate Score
```

## Running the Project

### Prerequisites

Make sure the following are installed:

* Java
* Maven
* PostgreSQL

### Start Services

Start the services in the following order:

```text
1. Service Registry
2. Question Service
3. Quiz Service
4. API Gateway
```

Each service can be started using Maven:

```bash
mvn spring-boot:run
```

Run the command from the respective service directory.

## Database

The project uses PostgreSQL for persistent storage.

Sample question data is provided in:

```text
question-table-data.sql
```

Configure the PostgreSQL connection details in the respective Spring Boot application configuration files before running the services.

## Future Improvements

* Add authentication and authorization using Spring Security/JWT
* Add centralized configuration using Spring Cloud Config
* Add Docker containerization
* Add Kubernetes deployment
* Add automated CI/CD pipeline
* Add centralized logging and monitoring

## Author

**Akash Gupta**

GitHub: [akashgupta2233](https://github.com/akashgupta2233/quiz-microservices-spring-boot)
