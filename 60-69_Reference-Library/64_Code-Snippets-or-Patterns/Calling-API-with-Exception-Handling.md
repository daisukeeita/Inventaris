---
id: Calling-API-with-Exception-Handling
aliases: []
tags:
  - code-snippet
  - exception-handling
  - api-handling
---

# Code Snippet - Calling-API-with-Exception-Handling

## Description

### Purpose

Calling the Third-Party API from DotEnv with handling the errors it'll throw.

**Returns**

- JSON Data of the Vehicle Inspection.

**Errors**

- 400 BAD_REQUEST
- 500 SERVICE_UNAVAILABLE

## Code

```java
public class VehicleApiDataFetcher implements VehicleClientInterface {

  private final Dotenv dotenv = Dotenv.load();
  private final String uri = dotenv.get("API_URI");
  private final RestTemplate restTemplate = new RestTemplate();

  @Override
  public VehicleInspection fetchVehicleData(VehicleRequest vehicleRequest) {
    try {
      final HttpHeaders header = new HttpHeaders();
      header.setContentType(MediaType.APPLICATION_JSON);
      final HttpEntity<VehicleRequest> payload = new HttpEntity<VehicleRequest>(vehicleRequest, header);

      ResponseEntity<VehicleInspection> response = restTemplate.postForEntity(uri, payload, VehicleInspection.class);

      return response.getBody();

    } catch (HttpClientErrorException exception) {
      if (exception.getStatusCode() == HttpStatus.BAD_REQUEST) {
        throw new VehicleResourceNotFoundException("Vehicle was not found in the LTMS database and Legacy data.");
      } else if (exception.getStatusCode() == HttpStatus.SERVICE_UNAVAILABLE) {
        throw new VehicleServiceNotAvailableException("Cannot connect to the LTMS.");
      } else {
        throw new UnexpectedError("An unexpected error occured in calling the LTMS.");
      }
    }
  }
}
```
