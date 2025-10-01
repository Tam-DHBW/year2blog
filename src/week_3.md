# Blog Entry 3 – Laying the groundwork

Hey guys!
This week we were finally done with organizational hassles and could start developing our game!

We were mainly concerned with building the basis to develop our application on and not with any features themselves yet.
This means getting everything required to run on AWS.

# Terraform
As mentioned in the previous blog post, we use terraform to manage our cloud infrastructure.
Terraform is a *Infrastructure as Code (IaC)* tool, meaning we can declare and configure all of our AWS components
using the *Hashicorp Configuration Language (HCL)*.
Doing so is really convenient, because we can commit our entire infrastructure to our project git repository,
and at any point we can redeploy this entire configuration on AWS.

For example, we had to switch over to a different AWS account, but this was not an issue at all, since we could just recreate all components using a single command.

To date, we have about 500 lines of terraform code managing ~30 cloud resources in total.

# Frontend
Check it out youself: https://d1ec4fqqusaq2g.cloudfront.net
|<img alt="image" src="https://github.com/user-attachments/assets/dd80667f-c37c-4965-81b6-af48375ddd9e" />|<img alt="image" src="https://github.com/user-attachments/assets/75bfcce9-b90a-49c0-8e81-68a8a604c22d" />|
|---|---|

The frontend is a Single-Page-Application built using React.
We went for an awesome looking retro theme, and to make it feel like a proper game we have sound effects and background music!

The chat page is currently not connected to any sort of backend yet,
however registration and login work like a charm.
For this we used AWS Cognito: It makes account management super easy, and we even get email account confirmation codes!

To host the website, we are using an AWS S3 bucket. Basically this is just cloud storage to which we upload the built React project.

# Backend
The backend does not have any features implemented yet, since this week we were only concerned with building foundations.

We decided on exposing the backend as a REST API. To do so we use the AWS Api Gateway to specify all API resources and their http methods.
The gateway then forwards API calls to an AWS Lambda, the cloud resource actually containing and running the API.
The benefit of using Lambda over a traditional deployment on some server is that we get automatic scaling.

We chose Rust as the language to implement the backend in, because it is very fast.
Less time spent running the backend equates to less time we get billed for!

A very nice development quality of life feature we implemented is the automatic generation of Api Gateway resources based on the Rust code in the backend.
Instead of manually creating an API route in both the backend and API Gateway, we define our whole routing table through a Rust macro like this:
```rust
api_routes! {
    ["abc", "def"] {
        GET --> handler_a;
        POST |-> handler_b;
    }
    ["user", (id: u8), "profile"] {
        GET --> hancler_c;
    }
}
```
> The arrow types `-->` and `|->` determine whether a user needs to be authenticated to call the api route

What the macro then does is
- Create a router for the backend handling the specified routes and
- Output the routes and methods as JSON for terraform to process

Now creating api routes is only half the work, and avoids having any inconsistencies between the backend and the API Gateway.

# Stringing it together
To make both our frontend and backend be accessible from the origin, we use an AWS Cloudfront Distribution.
Having both components on the same origin saves us from later running into any unexpected CORS headaches.
We then route requests according to the URL path:
- `/api/*` -> Forwarded to API gateway
- `/assets/*` -> Forwarded to asset folder in the frontend S3 Bucket
- `/*` -> Redirected to `index.html` in the frontend S3 Bucket

Cloudfront also provides us with caching and spans many geographic regions, ensuring our users have a great experience from anywhere in the world!

Thanks for reading and see you next week!
