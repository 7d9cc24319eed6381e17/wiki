# wiki

# How to build and run project locally
## Create personal github token
[https://help.github.com/en/github/authenticating-to-github/creating-a-personal-access-token-for-the-command-line]

You should activate `*:packages` permissions
## login in docker registry
```sh
docker login docker.pkg.github.com -u <GITHUB USERNAME>
# paste your token in password prompt 
```

## prepare run docker compose
Create .env.local file
```sh
git clone git@github.com:7d9cc24319eed6381e17/wiki.git && cd wiki/examples
cp .env .env.local
```

in `.env.local` you shall set manually 3 env vars. Contact @pwlae for values
```
SENDGRID_API_KEY=
ALERT_SERVICE_EMAIL_FROM=
IEX_TOKEN=
```

And then
```sh
docker-compose up
```

Front api service should be available on localhost:8080
```sh
curl -X POST \
  'http://localhost:8080/v1/123/stock/alerts?symbol=TSLA&client_id=test@mail.com&price=10.0' \
  -H 'cache-control: no-cache'

# => {"data":{"id":"5ec6c7a113b58955c43787ae","message":"alert has been created"}}%
```