# CodeReview BOT

> A code review robot powered by Bard

Translation Versions: [ENGLISH](./README.md) | [中文简体](./README.zh-CN.md) | [中文繁體](./README.zh-TW.md) | [한국어](./README.ko.md) | [日本語](./README.ja.md)

## Configuration

1. Go to the repo homepage which you want integrate this bot
2. click `settings`
3. click `actions` under `secrets and variables`
4. Change to `Secrets` tab, create a new variable `BARD_API_KEY` with the value of [your open api key](https://www.bardapi.dev/)

<img width="1052" alt="image" src="https://user-images.githubusercontent.com/13167934/218999459-812206e1-d8d2-4900-8ce8-19b5b6e1f5cb.png">

## Using Github Actions

[actions/bard-codereviewer](https://github.com/marketplace/actions/bard-codereviewer)

1. add the `BARD_API_KEY` to your github actions secrets
2. create `.github/workflows/cr.yml` add bellow content

```yml
name: Code Review

permissions:
  contents: read
  pull-requests: write

on:
  pull_request:
    types: [opened, reopened, synchronize]

jobs:
  test:
    if: ${{ contains(github.event.*.labels.*.name, 'gpt review') }} # Optional; to run only when a label is attached
    runs-on: ubuntu-latest
    steps:
      - uses: amondnet/bard-codereview@v0
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          BARD_API_KEY: ${{ secrets.BARD_API_KEY }}
          # Optional
          LANGUAGE: Korean
```

## Self-hosting

1. clone code
2. copy `.env.example` to `.env`, and fill the env variables
3. install deps and run

```sh
npm i
npm -i g pm2
npm run build
pm2 start pm2.config.cjs
```

[probot](https://probot.github.io/docs/development/) for more detail

## Dev

### Setup

```sh
# Install dependencies
npm install

# Run the bot
npm start
```

### Docker

```sh
# 1. Build container
docker build -t cr-bot .

# 2. Start container
docker run -e APP_ID=<app-id> -e PRIVATE_KEY=<pem-value> cr-bot
```

## Contributing

If you have suggestions for how cr-bot could be improved, or want to report a bug, open an issue! We'd love all and any contributions.

For more, check out the [Contributing Guide](CONTRIBUTING.md).

## Credit

this project is inpired by [CodeReview BOT](https://github.com/anc95/ChatGPT-CodeReview)
this project is inpired by [codereview.gpt](https://github.com/sturdy-dev/codereview.gpt)

## License

[ISC](LICENSE) © 2023 anc95
