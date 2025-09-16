---
id: Troubleshooting-Template
aliases: []
tags:
  - troubleshoot
involved-system:
  - backend
  - frontend
  - database
---

# Troubleshooting: {{title}}

## Description

### Symptoms

> [!TIP]
> What exactly was observed?
>
> > Example:
> > "Users reporting 500 error on product detail page."
> > "Application crashes after 10-minute uptime."
> > "Data not processing in database after form submission."

### Impact

> [!TIP]
> Who and what was affected?
> How server was it?

### Error Messages/Logs

```fish
java.lang.NullPointerException: Cannot invoke "com.sample.service.UserService
getUserById(java.lang.long)" because "this.userService" is null at
com.example.controller.UserController.getUser(UserController.java:35)
```

## Hypothesis

- Hypothesis 1: "Dependency Injection Failure."

## Investigation Steps and Findings

1. [HH:MM] Action: "Checked Application Logs on DEV environment."
   - Findings: "Saw `NullPointerException` at `UserController.java:35`."

## Root Cause

"The userService dependency in UserController was not correctly injected
by Spring's IoC container because the @Autowired annotation was missing.
Therefore, the field remained null, leading to a NullPointerException
when attempting to call a method on it."

## Solution

### Actions Taken

- Added `@autowired` annotation to the `UserService` field in `UserController`.

```java
// Before:
private UserService userService;

// After:
@Autowired // THIS WAS THE FIX //
private UserService userService;
```

### Verification

- Deployed fix to 'DEV', tested endpoint via browser/curl.
- Confirmed 200 OK and correct data.
- Checked logs for new errors.

## Lessons Learned / Key Takeaways

### Immediate Lesson

Always double-check `@Autowired` or other dependency injection annotations
when encountering `NullPointerException` related to service/component fields in Spring.

### General Principle

Systematically verify object initialization and dependency injection. Don't assume.

### Process Improvement

Could add a static analysis check (e.g., SonarQube rule) for
missing `@Autoowired` annotations on injected fields.
