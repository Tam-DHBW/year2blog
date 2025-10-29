# Blog Entry 7

### 1. Describe your chosen framework

For this project, I chose Axum, a modern and lightweight web framework for Rust. Axum focuses on type safety, performance, and modularity, leveraging Rust’s powerful async ecosystem (built on top of Tokio).

It follows a router-based design, where each route maps to a specific handler function. Handlers are typically asynchronous and use Rust’s strong typing system to ensure safe request and response handling at compile time.

Axum emphasizes composition rather than monolithic design — middleware, extractors, and layers can be flexibly combined to structure complex applications. It integrates well with Tower, enabling reusable components for logging, error handling, or authentication.

Unlike traditional frameworks like Django or Rails, Axum gives developers fine-grained control over the HTTP layer, making it particularly suitable for building high-performance APIs and microservices rather than large, template-driven web apps.

### 2. Does your framework generate simple CRUD (Create, Read, Update, Delete), and are you using this?

Axum does not include built-in CRUD generation tools. Unlike frameworks such as Laravel or Rails that automatically scaffold models and controllers, Axum requires developers to manually define routes, request handlers, and database logic.

### 3. Screencast of our demo 

<a href="https://drive.google.com/file/d/1QY9wxeYr1UjtRr0hpPu5w5Y3N2YBs7J3/view?usp=sharing" target="_blank">
  <img width=100% height=100% alt="Screenshot 2025-10-29 at 15 33 18" src="https://github.com/user-attachments/assets/3c197975-1a4d-428e-b45f-010d5c46b511" />
</a>

### 4. Architectural UML Diagram

<img width=100% height=100% alt="PNG image 2" src="https://github.com/user-attachments/assets/ebdb3d28-f389-45e5-96b1-3ba17ccdae95" />

For our project, we designed a web application that combines a React frontend with a Rust Axum backend, both running on AWS. The main goal of the architecture is to provide a secure, scalable, and serverless environment for handling user interactions with LLM.

The frontend is built with React and React Router to manage navigation within the app.
We used NES.css for styling and JavaScript for logic and interactivity.

The app is hosted in an S3 bucket, which serves static files (HTML, CSS, and JS). These files are distributed globally via CloudFront, making the website fast and reliable.

When a user opens the website:

	1.	CloudFront delivers the React app from the S3 bucket.
	2.	The app sends API requests to the backend through API Gateway.

The backend is completely serverless and built on top of AWS services:

	•	API Gateway acts as the main entry point for all API requests. It routes the requests to specific Lambda functions depending on the endpoint.
	•	Authorizer Lambda verifies JWT tokens issued by AWS Cognito. It makes sure only authenticated users can access protected routes and logs each request.
	•	The main backend logic is handled by Axum, a lightweight and high-performance Rust web framework running inside a Lambda function.
Axum defines the API routes and handler functions, which process user requests — for example, retrieving level data or saving player progress.


### 5. The RUP architecture document is filled out and online.

You can find it here:

- [Project description](./docs/project-description.md)
- [Tech stack](./docs/tech-stack.md)
- [Architecture](./docs/architecture.md)
- [Conventions](./docs/conventions.md)
- [RUP roles](./docs/rup-roles.md)
- [Software requirements specification](./docs/srs.md)
- [Use cases](./docs/use-cases/README.md)
    - [AI gatekeeper chat](./docs/use-cases/ai-chat.md)
    - [Level progression](./docs/use-cases/level-progression.md)
    - [Level selection](./docs/use-cases/level-selection.md)


### 6 MVC

### 6.1 MVC High level diagram 

<p align="center">
  <img src="https://github.com/user-attachments/assets/cf8b5754-01eb-4e7a-b66e-9d2e1ea9a982" width="50%" height="50%">
</p>
	 
### 6.2 MVC class diagram 
<p align="center">
  <img src="https://github.com/user-attachments/assets/8f121393-b083-45c8-89d4-a1284eaef255" width="75%%" height="75%">
</p>


