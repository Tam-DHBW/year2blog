# Blog Entry 7

### 1. Describe your chosen framework

For this project's backend, we chose Axum, a modern and lightweight web framework for Rust. Axum focuses on type safety, performance, and modularity, making use of Rust’s powerful async ecosystem.

It follows a router-based design, where each route maps to a specific handler function.

Since Axum is simple yet powerful, it provides us with a lot of flexibility and customizability for deploying to AWS.

### 2. Does your framework generate simple CRUD (Create, Read, Update, Delete), and are you using this?
No Axum does not include built-in CRUD generation tools.

This is however now a problem for our use case,
since most of the time DynamoDB queries are custom-tailored for the use case.

Only a single table exists in our application where CRUD generation could even be considered.

### 3. Screencast of our demo 
<iframe src="https://drive.google.com/file/d/1QY9wxeYr1UjtRr0hpPu5w5Y3N2YBs7J3/preview" width="640" height="480" allow="autoplay"></iframe>

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

### Cucumber
We also have cucumber running, though for now not yet on our website since it requires authentication to do anything
<img alt="image" src="https://github.com/user-attachments/assets/235bdf1f-0751-4561-8857-5d10935baa7c" />


### 6 MVC

### 6.1 MVC High level diagram 

<p align="center">
  <img src="https://github.com/user-attachments/assets/cf8b5754-01eb-4e7a-b66e-9d2e1ea9a982" width="50%" height="50%">
</p>
	 
### 6.2 MVC class diagram 
<p align="center">
  <img src="https://github.com/user-attachments/assets/8f121393-b083-45c8-89d4-a1284eaef255" width="75%%" height="75%">
</p>


