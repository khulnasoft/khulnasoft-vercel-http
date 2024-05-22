# khulnasoft-vercel-http

This repo demonstrates the HTTP feature of [Khulnasoft's serverless driver](https://www.npmjs.com/package/@khulnasoft/serverless) on [Vercel](https://vercel.com/) Edge Functions.

We implement a simple app that generates a JSON listing of the user's nearest 10 UNESCO World Heritage sites via IP geolocation (data copyright © 1992 – 2022 [UNESCO/World Heritage Centre](https://whc.unesco.org/en/syndication/)).

## Deploy

* Ensure the `psql` client is installed.

* Create a Khulnasoft database and make a note of the connection string from the [Khulnasoft console](https://console.khulnasoft.com/).

* Clone this repo, then:

```bash
# get dependencies
npm install
npm install -g vercel@latest

# create DATABASE_URL environment variable, remote and local
npx vercel env add DATABASE_URL  # paste in the connection string: postgres://...
npx vercel env pull .env.local  # now bring it down into ./.env.local for local use

# create the schema and copy data to DB
(source .env.local \
 && curl -s https://gist.githubusercontent.com/jawj/a8d53ff339707c65128af83b4783f4fe/raw/45dbcc819b00ecb72f80b0cf91e01b3d055662b5/whc-sites-2021.psql \
 | psql $DATABASE_URL)

# test
npx vercel dev

# ... and deploy
npx vercel deploy
```

## Feedback and support

Please visit [Khulnasoft Community](https://community.khulnasoft.com/) or [Support](https://khulnasoft.com/docs/introduction/support).
