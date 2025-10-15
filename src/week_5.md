# Blog Entry 5 – Working LLM Chats and Behaviour Driven Development

**Hey everyone, we at jAilbreak made big progress this week!**
### Authorization
First of all, we now have working authorization for our REST API.
The existence of users is managed for us by AWS Cognito.
After creating an account through this service, users are able to obtain a JWT access token from Cognito.
We have now implemented an authorizer which validates the JWT access token, and forwards the user-ID to our REST API
<img width="2156" height="1112" alt="image" src="https://github.com/user-attachments/assets/27a1dd01-ffc4-4821-a320-9f006ba70652" />

### LLM Conversations
Tricking a LLM into giving you the secret password is the crux of our game. No LLM, no game to play.
Luckily we were already able to implement such an essential feature this week.

The players chat with AI agents, which we give specific instructions and, of course, the secret password.
By default, agents created using AWS bedrock are already given quite a lot of instructions by default, which were surprisingly annoying to disable.
The default instructions made the agent return the same short boring rejection message at even the slightest hint malicious intent.
This made interacting with the agent super boring, and defeats the entire purpose of our game of course.
We managed to cleanse the prompts of these joy-killing instructions and are now able to chat much more freely with the models!

Currently we are using the smallest Llama 3.2 model for our responses, as it is pretty cheap.
There is also no real need for a sophisticated expensive model, since we dont want it to be super smart, it just has to be fun.

We did not just implement single prompt interactions, but fully fledged multi-turn conversations.
This means you dont have to obtain the password using a single message, but can instead have fun and take your time tricking the AI.

We generate these AI agents on-the-fly, allowing us to fully customize their behaviour on a per-level basis.

The responses from the AI are already super fast (~1 second), but we can still boost latency in the future

<img width="1510" height="361" alt="image" src="https://github.com/user-attachments/assets/07b804cb-af37-4b05-aa3d-80f7569e8dc7" />

We even have a quick-and-dirty frontend integration, so you can chat with our admittedly still very dumb gatekeeper right now => [🎮 jAilbreak](https://d1ec4fqqusaq2g.cloudfront.net)

<img width="883" height="658" alt="image" src="https://github.com/user-attachments/assets/d1c0319b-d89d-45f4-921a-7f5e7d82a739" />

### Behaviour driven development
We did the mandatory behaviour driven development using cucumber too of course.
So far we do not test our own site yet, since doing anything on our website requires authentication,
and we have not setup anything proper in that regard yet for testing porposes.

Instead we can say, with 100% accuraccy, that the google search bar *does indeed* exist:
```javascript
import { Given, When, Then, BeforeAll } from "cucumber"
import { Builder, By, Capabilities, Key, WebElementCondition } from "selenium-webdriver";

const capabilities = Capabilities.firefox();
const driver = new Builder().withCapabilities(capabilities).build();

BeforeAll(async function () {
    await driver.get("about:config")
})

Given("I am on google", async function () {
    await driver.get("https://google.com/")
})

Then("The search bar exists", async function () {
    await driver.findElement(By.css('form[action="/search"] textarea'))
})
```
<img width="713" height="142" alt="image" src="https://github.com/user-attachments/assets/933d13dd-c4a4-4a10-90cd-5b271cfaf7b1" />

---
## Thanks for reading and have fun teasing our gatekeeper!
