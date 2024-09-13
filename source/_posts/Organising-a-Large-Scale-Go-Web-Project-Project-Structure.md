---
title: 'Organising a Large-Scale Go Web Project: Project Structure'
lang: en
date: 2024-09-13 13:51:14
categories:
  - Leura
tags:
  - Software Architecture
---

## Reference

- [https://go.dev/doc/modules/layout](https://go.dev/doc/modules/layout)

## Introduction

Organising a large-scale Go web project is important for ensuring long-term maintainability, especially for open-source projects. Without a well-organised structure, it will be crazy hard to onboard new developers, fix bugs, and implement new features.

However, organising a Go project comes with its own challenges. Developers need to carefully consider how to structure their code and manage dependencies since there's no official recommendations on how to do that. This article comes my previous experience and explores best practices and strategies for organising a large-scale open-source Go web project, helping you build applications that are easy to maintain and scale from the ground up.

## The `internal/` Directory for Supporting Packages

The `internal/` directory is an essential part for organising a large-scale Go project with multiple supporting packages. It contains packages that are only used internally within this application and prevents other modules and applications from importing and depending on them.

This provides a safe way to encapsulate business logic, making the project more maintainable and avoiding unexpected dependencies.

Here's an example `internal/` directory:

```bash
internal/
  db/
    db.go
    db_test.go
    mongo.go
    mongo_test.go
    mysql.go
    mysql_test.go
  auth/
    auth.go
    auth_test.go
  service/
    user_service.go
    user_service_test.go
```

Here's the description of the directories listed above:

- `internal/db/`: Manages connections and queries for databases, encapsulating database logic in one package.
- `internal/auth/`: Contains logic for authorisation, like generating tokens, identifying permissions, and validating credentials.
- `internal/service/`: Implements web services, like user management, without exposing them outside this application.

### Unit Testing

Unit testing is a critical part of any large-scale project. The best practice for Go unit testing is to place tests alongside the files they test. Each package should have its corresponding `_test.go` files. For example:

```bash
internal/
  db/
    db.go
    db_test.go # Unit tests
```

## Single-Command Projects

While many large projects may consist of multiple commands, most web services, APIs, or server-side applications are designed with a single command (usually included in main.go) that serves as the entry point for the entire application.

Even with a single command, it's important to follow best practices for structuring the project, especially as it grows in scale.

### Basic Structure

Here's an example directory layout for a single-command large-scale Go project that consists of multiple packages:

```bash
root-directory/
  Makefile # Optional: to automate tasks like building and testing
  go.mod
  go.sum
  main.go # Entrypoint for the application
  internal/
    db/
      db.go
      db_test.go
    service/
      user_service.go
  # Reusable packages for shared logic
  hash/
    hash.go
    hash_test.go
  logger/
    logger.go
    logger_test.go
  # Other supporting directories with non-Go code...
```

### Reusable Packages

Reusable packages are intended for logic or services that are reusable outside the project. They may also contain packages that are reusable within the project, which is common in old projects. These packages usually handle tasks that are not tightly coupled with the application but provide generic functionality, such as logging and utilities.

However, a typical Go web project usually doesn't have anything to export since it's self-contained. In this case, it's recommended to keep all the packages inside the `internal/` directory to avoid unexpected dependencies.

## Multiple-Command Projects

Large Go web projects often involve multiple entrypoints or executables (i.e., commands); each has a specific purpose within the application.

For example, in a microservice architecture web application, there should be distinct services. Each of them needs its own entrypoint (i.e., main function).

### Basic Structure

In projects with multiple executables, the best practice is to separate each command into its own directory within the project to avoid potential conflicts. A common convention is to put all commands in the `cmd/` directory, which ensures a clear difference between the executable files and supporting packages.

Here's an example directory layout for a multiple-command large-scale Go project:

```bash
root-directory/
  Makefile # Useful in multiple-command projects
  go.mod
  go.sum
  cmd/
    service1/
      main.go
    service2/
      main.go
  internal/ # Shared internal packages
    db/
      db.go
      db_test.go
    utils/
      utils.go
  # Other supporting directories with non-Go code...
```

### Makefile

With multiple commands in the same project, it's essential to have a structural and easy-to-maintain build process.

Here's an example Makefile for the directory layout above to simplify the build process:

```makefile
build-service1:
		go build -o build/service1 ./cmd/service1

build-service2:
		go build -o build/service2 ./cmd/service2

.PHONY build-service1 build-service2
```

## Conclusion

Organising a large-scale Go web project involves more than just code. By organising the project in a scalable and maintainable way—using directories like `internal/` and `cmd/` —we create a foundation that is clear and sustainable.

This helps teams, especially open-source project collaborators, collaborate more effectively, reduct human mistake, and ensures maintainability and sustainability.
