# GIT

> **Notez Bien**: All these rules are meant to be broken, **BUT** you need a very good reason **AND** you must explain it in a comment.

## TL;DR

Follow guidelines in [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/).

The commit message should be structured as follows:

```text
<type>[optional scope]: <short description>

[optional long description(s)]

[optional specification(s)]
```

### Type

* **build**: Changes that affect the build system or external dependencies (example scopes: gulp, broccoli, npm)
* **ci**: Changes to our CI configuration files and scripts (example scopes: Travis, Circle, BrowserStack, SauceLabs)
* **docs**: Documentation only changes
* **feat**: A new feature
* **fix**: A bug fix
* **perf**: A code change that improves performance
* **refactor**: A code change that neither fixes a bug nor adds a feature
* **style**: Changes that do not affect the meaning of the code (white-space, formatting, missing semi-colons, etc)
* **test**: Adding missing tests or correcting existing tests

Use a bang `!` after type to draw attention, e.g., to breaking change. 

### Specification

