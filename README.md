## Deploy to Fly

Install the Fly CLI tool:

```sh
brew install flyctl
```

Authenticate the CLI:

```sh
fly auth login
```

Launch the app:

```sh
fly launch
```

Follow the prompts by `fly launch` and make sure to answer them in the following way:

```sh
? Would you like to copy its configuration to the new app? Yes
? Choose an app name (leaving blank will default to 'trigger-v2-fly-demo') <enter your preferred app name here or leave blank>
? Would you like to set up a Postgresql database now? Yes
? Would you like to set up an Upstash Redis database now? No
? Would you like to deploy now? No
```

If you plan on logging in with GitHub auth, you'll need to create a GitHub OAuth app with the following configuration:

We use Resend for email sending, they have a generous free tier of 100 emails a day that should be sufficient. Signup for Resend and enter the required environment vars below

Set the necessary secrets:

```sh
fly secrets set \
  MAGIC_LINK_SECRET=<random string> \
  SESSION_SECRET=<random string> \
  LOGIN_ORIGIN="https://<fly app name>.fly.dev" \
  APP_ORIGIN="https://<fly app name>.fly.dev" \
  FROM_EMAIL="Acme Inc. <hello@yourdomain.com>" \
  REPLY_TO_EMAIL="Acme Inc. <reply@yourdomain.com>" \
  RESEND_API_KEY=<your API Key> \
  AUTH_GITHUB_CLIENT_ID=<your GitHub OAuth Client ID> \
  AUTH_GITHUB_CLIENT_SECRET=<your GitHUb OAuth Client Secret>
```

Now you can deploy:

```sh
fly deploy --vm-size performance-1x
```
