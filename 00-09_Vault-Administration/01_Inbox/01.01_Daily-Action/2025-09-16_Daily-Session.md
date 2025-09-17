---
id: 2025-09-16_Daily-Session
aliases: []
tags:
  - daily-actions
date: "2025-09-16"
---

# 2025-09-16 Daily-Session Log

## Goal/s

> [!TODO]- Personal Tasks
>
> - [ ] Research for running preparations.

> [!TODO]- Professional Tasks
>
> - [x] Apply the Exception Handling for third-party API.
>   > - [x] Document the code snippet/s to my personal vault.
> - [x] Sort the Exception Handling in Service Layer.

> [!TODO]- Work Tasks
>
> - [x] Update the Daily PMVIC Uploads Report.

---

## Session Log/s

### Activity 1: Exception Handling for Third-Party API

**START**: 10:06AM
**END**: 11:29AM

#### Commands/Codes used

- [[Calling-API-with-Exception-Handling]]

### Activity 2: Documenting the Exception Handling for Third-Party API

**START**: 11:33AM
**END**: 11:42AM

### Activity 3: Fix the Exception Handling in Service Layer

**START**: 12:30PM
**END**: 3PM -ish

---

## Reflection

### Results

> [!SUCCESS] Task 1
> I successfully handled the exception that the Third-Party API will throw.

> [!SUCCESS] Task 2
> Successfully documented exception handling in fetching a JSON Data from
> Third-Party API.

> [!SUCCESS] Task 3
> Successfully fixed and sorted the exception handling in Service Layer.
> Though, I still need to document the implementation of my feature.

### Things that I learned

I've learned Exception Handling in Spring Boot. Once you've implemented a Global
Exception Handler with `@RestControllerAdvice` or `@ControllerAdvice`, throwing
an Exception class will automatically send this as HTTP Status to the client
with customized JSON body, if implemented.
