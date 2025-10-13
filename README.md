# WhatsApp Demo For Text-Based Customer Service

<img src="https://developer.nexmo.com/assets/images/Vonage_Nexmo.svg" height="48px" alt="Nexmo is now known as Vonage" />

This is a basic demo app routing user enquiries to customer service people, all via WhatsApp

[![Deploy](https://www.herokucdn.com/deploy/button.svg)](https://heroku.com/deploy)

## Prerequisites

* A Vonage account, [sign up for a new account here](https://dashboard.nexmo.com/sign-up?utm_source=DEV_REL&utm_medium=github&utm_campaign=text-based-whatsapp-callcenter) if you don't have one already
* **EITHER** a WhatsApp Business number **OR** you can try this app using the [Messages API Sandbox](https://developer.nexmo.com/messages/concepts/messages-api-sandbox) - but only telephone numbers that you whitelist through the dashboard can be used. This makes the sandbox ideal for testing with a controlled group of numbers.
* NodeJS and NPM
* Redis

## Set up the application to run locally

1. Create a messages application and set the incoming message and message status webhooks to point to `[APP URL]/webhooks/inbound` and `[APP URL]/webhooks/status` respectively. See also: [Creating a Messages API Application](https://developer.nexmo.com/messages/code-snippets/create-an-application)
2. If you are using the Messages Sandbox, then also configure the sandbox URLs for Messages to point to (the same URLs as used in the application) `[APP URL]/webhooks/inbound` and `[APP_URL]/webhooks/status` respectively.
  - Your application must be publicly available. If running locally, you might find our [guide to using Ngrok for development](https://developer.nexmo.com/tools/ngrok) helpful.
3. Clone this repo, and run `npm install`
4. Create a `.env` file (see variables below)
5. Add your configuration values to the `.env` file, this will include the connection details for your Redis instance and your Vonage credentials including an application and private key. The private key should be pasted on one line with all newlines replaced with `\n`
6. Run `npm start` in your terminal

### Running Redis with Docker

If you don't have Redis installed locally, you can start one with Docker:

```bash
docker compose up -d redis
```

This will expose Redis on `localhost:6379`. Set `REDIS_URL=redis://localhost:6379` in your `.env`.

### Environment Variables

```
REDIS_URL=redis://localhost:6379
VONAGE_API_KEY=your_key
VONAGE_API_SECRET=your_secret
VONAGE_APPLICATION_ID=your_app_id
VONAGE_APPLICATION_PRIVATE_KEY=path-to-your-private-key
```

## Using the app

> Note that all participants must first whitelist their numbers with the Messages Sandbox. You can [find more information about the Messages Sanbox on the Developer Portal](https://developer.nexmo.com/messages/concepts/messages-api-sandbox)

* Your agent numbers can send the message "sign in" to the WhatsApp number, the WhatsApp number will respond back that they have signed in.
* Your customer numbers will then message the same number with their questions or requests.
* Customer messages will be forwarded to the appropriate agent with an emoji prepended to the message. This feature allows the agent to handle multiple conversations simultaneously in a single whatsapp conversation.
* Agents respond to the WhatsApp conversation, with the appropriate emoji at the beginning of their message and the message will be routed to the correct cuser
* If the Agent sends a "sign out" message, their customers will be reallocated to available agents. If there are no available agents then the customer will be notified that there are no available agents.

## Getting Help

We love to hear from you so if you have questions, comments or find a bug in the project, let us know! You can either:

* Open an issue on this repository
* Join the Vonage Community Slack](https://developer.vonage.com/community/slack)

## Further Reading

* Check out the Developer Documentation at <https://developer.vonage.com>
* More information about the Messages API Sandbox: <https://developer.vonage.com/messages/concepts/messages-api-sandbox>

