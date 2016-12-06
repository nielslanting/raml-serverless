# RAML-Serverless Plugin

Generate [RAML](http://raml.org/) documentation for [Serverless](https://serverless.com/) projects.

This is a work in progress. Please check Github issues ([/andrewcurioso/raml-serverless/issues](https://github.com/andrewcurioso/raml-serverless/issues)) for a feature roadmap and consider contributing.

## Installation
1. Open a terminal to your Serverless project
2. `npm i --save 'https://github.com/andrewcurioso/raml-serverless'`
3. Add `raml-serverless` to your `serverless.yaml` file (see [Serverless docs](https://serverless.com/framework/docs/providers/aws/guide/plugins/#installing-plugins))

## Usage

Example usage:

```bash
sls raml > docs.raml
```

RAML-Serverless will automatically create a section of the documentation for each HTTP endpoint you have in your `serverless.yml` file.

You can put global documentation in the `custom:` object in your Yaml file and it will be copied as is into the output RAML. Anything that can go into a RAML file can go here. For example:

```yaml
custom:
  documentation:
    raml:
      title: My Awesome API
      version: v1.0
```

Which will result in a RAML file that starts with:

```yaml
#%RAML 1.0
title: My Awsome API
version: v1.0
```

You can also put RAML on individual HTTP event endpoints and they will be included in the output. For example:

```yaml
functions:
  index:
    handler: handlers.index
    events:
      - http:
          path: /hello
          method: get
          cors: true
          documentation:
             raml:
               description: Say hello to the world
```

Will produce this output in your RAML file:
```yaml
/hello:
  get:
    description: Say hello to the world
```

You can also include your RAML in a seperate file and import it into your `serverless.yml` using variables:

```yaml
custom:
  documentation:
    raml: ${file(raml-base.yml)}
```

## Contributing

This plugin is a work in progress. If you would like to contribute, go to Github issues ([/andrewcurioso/raml-serverless/issues](https://github.com/andrewcurioso/raml-serverless/issues)) and pick and issue to work on or create a new issue.