---
id: MultipleErrorStatusWrapInOneClass
aliases: []
tags:
  - code-snippet
topic:
  - topic
---

# Code Snippet - MultipleErrorStatusWrapInOneClass

## Description

### Purpose

Wrapping expected multiple exceptions into on Exception Class to reduce
redundancy.

### Context

- This can be used in:
  - Client Layer
  - Repository Layer
  - Service Layer

- Expected errors in a features or layers.

## Code

```java
  @ExceptionHandler(VehicleFileHandlingException.class)
  public ResponseEntity<ErrorResponse> handleVehicleFileExceptions(
      final VehicleFileHandlingException exception) {

    final Throwable cause = exception.getCause();
    final HttpStatus status = mapExceptionsToHttpStatus(cause);
    final ErrorResponse errorResponse = new ErrorResponse(status.value(), exception.getMessage());

    return ResponseEntity.status(status).body(errorResponse);
  }

    private HttpStatus mapExceptionsToHttpStatus(final Throwable cause) {
    if (cause instanceof FileNotFoundException) {
      return HttpStatus.NOT_FOUND;
    } else if (cause instanceof EOFException) {
      return HttpStatus.BAD_REQUEST;
    } else if (cause instanceof InterruptedIOException) {
      return HttpStatus.REQUEST_TIMEOUT;
    }

    return HttpStatus.INTERNAL_SERVER_ERROR;
  }
```
