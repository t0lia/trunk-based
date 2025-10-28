# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Spring Boot application (version 3.1.4) using Java 21, organized as a Maven multi-module project. The project structure uses a parent POM at the root level with the actual application module in the `app/` directory.

## Build & Development Commands

### Building the Project
```bash
# Build the entire project (from root)
./mvnw clean install

# Build only the app module
./mvnw -pl app clean install

# Package the application as a JAR
./mvnw package
```

### Running the Application
```bash
# Run from the app directory
cd app && ../mvnw spring-boot:run

# Or run from root targeting the app module
./mvnw -pl app spring-boot:run
```

### Testing
```bash
# Run all tests
./mvnw test

# Run tests for specific module
./mvnw -pl app test

# Run a single test class
./mvnw -Dtest=AppApplicationTests test
```

## Architecture

### Module Structure
- **Root POM** (`pom.xml`): Parent POM that defines the project structure
- **app module** (`app/`): Contains the Spring Boot application with artifact ID `app-backend`
  - Main application class: `com.apozdniakov.app.AppApplication`
  - Standard Maven directory layout: `src/main/java`, `src/main/resources`, `src/test/java`

### Spring Boot Configuration
- Spring Boot version: 3.1.4
- Java version: 21
- Dependencies:
  - `spring-boot-starter-web`: For RESTful web services
  - `spring-boot-starter-test`: For testing support
- Application entry point: `com.apozdniakov.app.AppApplication`

### Maven Multi-Module Setup
The project uses a parent-child module structure. When working with this codebase:
- Changes to the root `pom.xml` affect all modules
- The app module references the parent with `<relativePath>..</relativePath>`
- Version is inherited from parent: `0.0.1-SNAPSHOT`

## Maven Wrapper
This project uses Maven Wrapper (`mvnw`/`mvnw.cmd`), so Maven doesn't need to be installed globally. Always use `./mvnw` instead of `mvn` commands.
