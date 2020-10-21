# Bytebank web API

Spring Boot Web API for consumption of the Bytebank Flutter App

## Functionalities

The Web API offers the following features:

- Listing and registration of transactions.

## How to run

Open the terminal or prompt and access the ** server.jar ** file, then run the following command:

```
java -jar server.jar
```

> The project was built based on Java 8, so it is recommended to use Java 8 so that everything works as expected.

## Modifying startup properties
By default Spring Boot will run the application on port `8080` and will set the default password to` 1000` to save transactions.

If you want to modify both values, execute the file as follows:

```
java -jar server.jar --server.port=8081 --user.password=2000
```

>In this sample the web api will run on port `8081` with the transaction password` 2000`

## End-point mapping

To access the functionalities, the following end-points were made available:

- `/transactions`:
  - **GET**: List:
    - The result is ordered by the creation date and time in ascending order.

  ```
  // response example
  [
      {
          "id": "b9663ef3-3749-400e-be8f-1280db94aac8",
          "value": 200.00,
          "contact": {
              "name": "gui",
              "accountNumber": 1000
          },
          "dateTime": "2019-11-06 12:57:23"
      },
      {
          "id": "d1bf689c-caa2-4e45-b1fc-5a90b10d6d48",
          "value": 200.00,
          "contact": {
              "name": "gui",
              "accountNumber": 1500
          },
          "dateTime": "2019-11-06 12:57:37"
      }
  ]
  ```

  - **POST**: Insert:   
    - To save the transaction it is necessary to send the * header * `password` according to the value configured in the application:
      - If not sent, `400 BAD REQUEST` is returned;
      - If `401 UNAUTHORIZED` authentication fails.
    - It is not possible to change the transaction if `409 CONFLICT` is attempted.

  ```
  // request body example
  {
    	"value": 200.0,
    	"contact": {
    		"name": "gui",
    		"accountNumber": 1000
    	}
  }

  // response example
  {
        "id": "b9663ef3-3749-400e-be8f-1280db94aac8",
        "value": 200.00,
        "contact": {
            "name": "gui",
            "accountNumber": 1000
        },
        "dateTime": "2019-11-06 12:57:23"
  }
  ```
