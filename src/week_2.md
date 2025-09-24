# Blog Entry 2 – Team and Technology: jAilbreak

Hey everyone!  

In this second blog post, we’re excited to share the **high-level architecture** of *jAilbreak* and the **tech stack** we chose to build it.

welcome our team: 

## Team

| <img width="20%" height="20%" alt="image" src="https://github.com/user-attachments/assets/9a1a4476-c533-4d52-84b9-f81cc0ea6fac" /> | <img width="20%" height="20%" alt="image" src="https://github.com/user-attachments/assets/750a6594-bf53-4a60-9e12-658bbd45c970" />| 
|-------------------------------------------------------------------------|------------------------------------------------------------------|
|Bogdan                                                                   |Tamino                                                            | 
|FrontEnd Master and AWS god                                              |Rust Enjoyer and BackEnd superhero                                |

<bt></br>


## 🛠 High-Level Architecture  

Here’s how everything fits together:  

1. **Player Browser → CloudFront CDN (via HTTPS)**  
   Players interact with *jAilbreak* through their browsers. All traffic is routed securely over HTTPS to **Amazon CloudFront**.  

2. **Static Website Hosting on S3**  
   Our frontend assets (built with React and TypeScript) are hosted on **Amazon S3**.  

3. **API Gateway**  
   Requests that require backend processing (e.g., game state updates, scoring) are forwarded from CloudFront to **Amazon API Gateway**, which acts as the central entry point for all API calls.  

4. **AWS Lambda Backend**  
   Behind the gateway, **AWS Lambda** functions power the core game logic, session management, and analytics. This serverless approach keeps our backend lightweight and cost-effective while automatically scaling with demand.  

5. **Bedrock LLM AI**  
   Integrated with the Lambda backend, **Amazon Bedrock** provides an LLM-based AI that drives dynamic interactions, making the game world more intelligent and responsive.  

6. **DynamoDB + Safety Middleware**  
   Game state, player sessions, and analytics data are stored in **Amazon DynamoDB**. A safety filter middleware ensures that all AI outputs are moderated for appropriate content and fair gameplay.  

---

## 🛠 Tech Stack  

For the **tech stack**, we selected technologies that balance performance, scalability, and developer productivity:  

- **Frontend**  
  - TypeScript  
  - React  

- **Backend**  
  - AWS (Lambda, API Gateway, CloudFront, S3)  
  - DynamoDB for persistent storage  

- **Infrastructure as Code**  
  - Terraform  

- **Programming Language for Backend Logic**  
  - Rust  

<img width="100%" height="100%" alt="image" src="https://github.com/user-attachments/assets/1951bbff-3f13-449e-a198-edfaebb417e7" />

{{ #include comments.md }}
