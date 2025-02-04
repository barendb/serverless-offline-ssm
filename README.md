# serverless-offline-ssm
[![Build Status](https://travis-ci.org/janders223/serverless-offline-ssm.svg?branch=master)](https://travis-ci.org/janders223/serverless-offline-ssm)

This [Serverless](https://github.com/serverless/serverless) plugin allows you to develop offline while using AWS SSM parameters in your `serverless.yml` template. The plugin looks for environment variables which are fulfilled by SSM parameters at build time and substitutes them from a `.env` file when running locally with the [serverless-offline plugin](https://github.com/dherault/serverless-offline).

## Documentation

- [Installation](#installation)
- [Configuration](#configuration)
- [Contributing](#contributing)
- [License](#license)

## Installation

First install the plugins using npm or yarn

```bash
npm install serverless-offline serverless-offline-ssm --save-dev

#or

yarn add -D serverless-offline serverless-offline-ssm
```

Then inside of your project's `serverless.yml` file add the following to the plugins section. Note it is important that `serverless-offline-ssm` is loaded before `serverless-offline`. This is important to ensure that we are setting the variables properly for `serverless-offline` before it needs them.

_NOTE:_ It is imperative that `serverless-offline-ssm` be the the first plugin listed in the plugins section of your `serverless.yml` file. Due to the load order of plugins, other plugins may interfere with the loading of your `.env` file.

```yaml
plugins:
    - serverless-offline-ssm
    - serverless-offline
```

## Configuration

You can choose to use a `.env` file or define your variables in
`serverless.yml`. `serverless-offline-ssm` will always check if the
section `custom.serverless-offline-ssm` have any values, if not it will
fallback to `.env`

### .env

Your `.env` file needs to contain only variable names without the `ssm:` prefix and `~(true|false|split)` sulfix.

If you've defined `${ssm:lambda.LAMBDA_NAME.DB_DSN~true}` in `serverless.yml` file your `.env` need to be like the example bellow:

```
lambda.LAMBDA_NAME.DB_DSN="VAR VALUE"
```

### serverless.yml

```yaml
custom:
  serverless-offline-ssm:
    'lambda.LAMBDA_NAME.DB_DSN': 'sample-value-goes-here'
    'another.sample.value': '99 red baloons'
```

## Contributing

Pull requests are always welcome. Please see the [contributing](https://github.com/janders223/serverless-offline-ssm/blob/master/CONTRIBUTING.md) guidelines.

## License

[MIT](https://github.com/janders223/serverless-offline-ssm/blob/master/LICENSE)
