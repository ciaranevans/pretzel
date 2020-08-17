# pretzel 🥨☁️ ![Master Status](https://github.com/ciaranevans/pretzel/workflows/CI/badge.svg?branch=master)

_An AWS Serverless application within a monorepo_

---

The idea behind `pretzel` is to try and provide an example of a AWS hosted serverless application that is contained within a monorepo.

`pretzel` will comprise of:

* Automated Builds
* Automated Tests
    * Unit
    * Integration
* Automated Deployments
* CI/CD

_The name Pretzel was decided when A: I renamed it from MoSeX (Monorepo Serverless eXample) and B: when I found this gif:_

![Pretzel Making Bot](https://media.giphy.com/media/bwmYGtDbRCJyg/giphy-downsized.gif)

# Development - Setup and useful commands

<details>
<summary><b>Dependencies</b></summary>
Ensure the following system dependencies are in place:

* Python 3.8+ (I recommend using [pyenv](https://github.com/pyenv/pyenv))
* Node Version Manager [Here](https://github.com/nvm-sh/nvm)
* Pipenv [Here](https://github.com/pypa/pipenv) - Make sure you set:
    ```bash
    export PYENV_ROOT=<root/to/pyenv/install>
    export PIPENV_PYTHON=$PYENV_ROOT/shims/python
    ```
* AWS CLI [Here](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-install.html)
* AWS CDK `npm install -g aws-cdk`
* A file named `.env` with a value for `ENV`
    ```bash
    $ cat .env
    ENV=my-dev-env
    ```
</details>

<details>
<summary><b>Setup commands</b></summary>
Before you can develop, make sure you've run:

* `nvm install` - To setup Node and use the correct version
* `pipenv install -d` - To initialise the pipenv virtual environment and install the project dependencies
* `aws configure` - To setup the AWS CLI
</details>

<details>
<summary><b>Makefile</b></summary>

A Makefile is provided to make common tasks easier, the available commands are:

**`make lint`**

This will perform a dry run of `flake8`, `isort`, and `black` and let you know what issues were found

**`make format`**

This will perform a run of `isort` and `black`, this **will** modify files if issues were found

**`make unit`**

This will use `pytest` to run all unit tests found within `tests/unit`

**`make integration`**

This will use `pytest` to run all integration tests found within `tests/integration`

**`make diff`**

This will run a `cdk diff` using the value of `ENV` in your `.env` file to determine if there are any changes between your local stack definition and that of the the deployed instance (There may not be one, so everything will be new)

**`make deploy`**

This will run a `cdk deploy` using the value of `ENV` in your `.env` file to deploy your local stack definition to AWS

**`make destroy`**

This will run a `cdk destroy` using the value of `ENV` in your `.env` file to destroy your deployed stack

### Makefile combos

Makefile commands can be linked together, before pushing a commit/preparing to make a PR I'd recommend running:

`make format unit` - This will catch little formatting errors that are annoying to find out about when waiting for CI builds. It will also ensure that your tests pass and there's no silly mistakes laying around!

To fully run an integration test, an AWS deployment is required to hit, for this, I recommend running:

`make deploy integration destroy` - This will deploy the environment, run the tests then destroy it.
</details>
