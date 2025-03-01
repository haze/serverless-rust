# serverless rust [![Build Status](https://github.com/softprops/serverless-rust/workflows/Main/badge.svg)](https://github.com/softprops/serverless-rust/actions) [![npm](https://img.shields.io/npm/v/serverless-rust.svg)](https://www.npmjs.com/package/serverless-rust)


> A ⚡ [Serverless framework](https://serverless.com/framework/) ⚡ plugin for [Rustlang](https://www.rust-lang.org/en-US/) applications 🦀

## 📦 Install

Install the plugin with npm

```sh
$ npm i -D serverless-rust
```

💡 This serverless plugin assumes you are building Rustlang lambdas targeting the AWS Lambda "provided" runtime. The [AWS Lambda Rust Runtime](https://github.com/awslabs/aws-lambda-rust-runtime) makes this easy.

Add the following to your serverless project's `serverless.yml` file

```yaml
service: demo
provider:
  name: aws
  runtime: rust
plugins:
  # this adds informs serverless to use
  # the serverless-rust plugin
  - serverless-rust
# creates one artifact for each function
package:
  individually: true
functions:
  test:
    # handler value syntax is `{cargo-package-name}.{bin-name}`
    # or `{cargo-package-name}` for short when you are building a
    # default bin for a given package.
    handler: your-cargo-package-name
    events:
      - http:
          path: /test
          method: GET
```

> 💡 The Rust Lambda runtime requires a binary named `bootstrap`. This plugin renames the binary cargo builds to `bootstrap` for you before packaging. You do **not** need to do this manually in your Cargo configuration.

## 🖍️ customize

You can optionally adjust the default settings of the dockerized build env using
a custom section of your serverless.yaml configuration

```yaml
custom:
  # this section allows for customization of the default
  # serverless-rust plugin settings
  rust:
    # flags passed to cargo
    cargoFlags: '--features enable-awesome'
    # custom docker tag
    dockerTag: 'some-custom-tag'
```

### 🎨 Per function customization

If your serverless project contains multiple functions, you may sometimes
need to customize the options above at the function level. You can do this
by defining a `rust` key with the same options inline in your function
specification.

```yaml
functions:
  test:
    rust:
      # function specific flags passed to cargo
      cargoFlags: '--features enable-awesome'
    # handler value syntax is `{cargo-package-name}.{bin-name}`
    # or `{cargo-package-name}` for short when you are building a
    # default bin for a given package.
    handler: your-cargo-package-name
    events:
      - http:
          path: /test
          method: GET
```

## 🤸 usage

Every [serverless workflow command](https://serverless.com/framework/docs/providers/aws/guide/workflow/) should work out of the box.

### invoke your lambdas locally

```sh
$ npx serverless invoke local -f hello -d '{"hello":"world"}'
```

### deploy your lambdas to the cloud

```sh
$ npx serverless deploy
```

### invoke your lambdas in the cloud directly

```sh
$ npx serverless invoke -f hello -d '{"hello":"world"}'
```

### view your lambdas logs

```sh
$ npx serverless logs -f hello
```


## 🏗️ serverless templates

### ^0.2.*

* a minimal echo application - https://github.com/softprops/serverless-aws-rust
* a minimal http application - https://github.com/softprops/serverless-aws-rust-http
* a minimal multi-function application - https://github.com/softprops/serverless-aws-rust-multi
* a minimal apigateway websocket application - https://github.com/softprops/serverless-aws-rust-websockets
* a minimal kinesis application - https://github.com/softprops/serverless-aws-rust-kinesis

### 0.1.*

Older versions targeted the python 3.6 AWS Lambda runtime and [rust crowbar](https://github.com/ilianaw/rust-crowbar) and [lando](https://github.com/softprops/lando) applications

* lando api gateway application - https://github.com/softprops/serverless-lando
* multi function lando api gateway application - https://github.com/softprops/serverless-multi-lando
* crowbar cloudwatch scheduled lambda application - https://github.com/softprops/serverless-crowbar

Doug Tangren (softprops) 2018-2019
