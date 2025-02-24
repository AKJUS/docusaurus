# Api reference 

Description of all avaliable routes you can send HTTP requests to for Threadbag.  



This document provides a detailed reference for the Threadbag API, including endpoints, request/response structures, and examples.

\---

## Base URL

All endpoints are relative to the base URL:

[http://localhost:8081](http://localhost:8081/)



\---

## Endpoints

### 1. Get Application Info

**Endpoint:** `/`

**Method:** `GET`

**Description:**
Returns a link to the Threadbag documentation.

**Response:**
- **Body:** A string containing the documentation URL.

**Example:**

```bash
curl -X GET http://localhost:8081/
```

**Response:**


Threadbag Documentation: https://docs.bagpipes.io/docs/api/threadbag

* * *

### 2\. Get current Version

**Endpoint:** `/version`

**Method:** `GET`

**Description:**
Returns the current version of the deployed version.

**Response:**

-   **Body:** A string containing the version number.
**Example:**

```bash
curl -X GET http://localhost:8081/version
```

**Response:**

1.0.0

* * *

### 3\. List Open HRMP Channels (Polkadot)

**Endpoint:** `/polkadot/openchannels`

**Method:** `POST`

**Description:**
Lists open HRMP (Horizontal Relay-routed Message Passing) channels for a given parachain ID.
_Currently a placeholder implementation._

**Response:**

-   **Body:** A string indicating the endpoint is a work in progress.

**Example:**

```bash
curl -X POST http://localhost:8081/polkadot/openchannels
```

**Response:**

Todo!

* * *

### 4\. Broadcast Transaction

**Endpoint:** `/broadcast`

**Method:** `POST`

**Description:**
Broadcasts a pre-signerd transaction to a specified chain.
_Currently a placeholder implementation._

**Example Request Body:**

```json
{
  "chain": "hydradx",
  "tx": "<transaction\_data>"
}
```

**Response:**

```json
{
  "status": "fail",
  "hash": "not found"
}
```


**Example:**
```bash
curl -X POST -H "Content-Type: application/json" -d '{"chain": "hydradx", "tx": "0xtxhere"}' http://localhost:8081/broadcast
```

* * *

### 5\. Save URL

**Endpoint:** `/saveUrl`

**Method:** `POST`

**Description:**
Saves a long URL and returns a shortened version.

**Request Body:**

```json
{
  "longurl": "<long\_url>"
}
```

**Response:**

```json
{
  "success": true,
  "shortUrl": "<shortened\_url>"
}
```

**Example:**

```bash 
curl -X POST -H "Content-Type: application/json" -d '{"longurl": "https://example.com"}' http://localhost:8081/saveUrl
```
* * *

### 6\. Get URL

**Endpoint:** `/getUrl/{name}`

**Method:** `GET`

**Description:**
Retrieves the original long URL associated with a shortened URL.

**Path Parameters:**

-   `name`: The shortened URL identifier.
**Response:**

```json
{
  "success": true,
  "longUrl": "<original_url>"
}
```

**Example:**
```bash
curl -X GET http://localhost:8081/getUrl/short_id
```

* * *

### 7\. XCM Asset Transfer

**Endpoint:** `/xcm-asset-transfer`

**Method:** `POST`

**Description:**
Initiates an XCM (Cross-Consensus Messaging) asset transfer.
_Currently a placeholder implementation._

**Response:**

Todo!

**Example:**
```
curl -X POST http://localhost:8081/xcm-asset-transfer
```
* * *

### 8\. Start Job

**Endpoint:** `/job/start`

**Method:** `POST`

**Description:**
Starts a scenario worker with the specified sceneraio id.

**Request Body:**

```json
{
  "id": "<scenario_id>",
}
```

**Response:**

```json
{
  "success": true,
  "result": "Job started"
}
```


**Example:**

```bash
curl -X POST -H "Content-Type: application/json" -d '{"id": "H!Xz6LWg", "delay": 12}' http://localhost:8081/job/start
```


* * *

### 9\. Stop Job

**Endpoint:** `/job/stop`

**Method:** `POST`

**Description:**
Stops a running scenario worker.

**Request Body:**

```json
{
  "id": "<scenario_id>"
}
```


**Response:**

```json
{
  "success": true,
  "result": "Job stopped"
}
```

**Example:**

```bash
curl -X POST -H "Content-Type: application/json" -d '{"id": "H!Xz6LWg"}' http://localhost:8081/job/stop
```

* * *

### 10\. Get Scenario Transactions

**Endpoint:** `/scenario/tx`

**Method:** `POST`

**Description:**
Retrieves all the transactions that has been generated for the scenario worker.  

**Request Body:**

```json
{
  "id": "<scenario_id>"
}
```


**Response:**

```json

{
  "mempool": [
    {
      "source_chain": "polkadot",
      "source_address": "5GdvmQtUwByTt6Vkx41vtWvg5guyaH3BL2yn6iamg1RViiKD",
      "dest_chain": "assetHub",
      "dest_address": "5D7RT7vqgZKUoKxrPMihNeXBzhrmWjd5meprfUFhtrULJ4ng",
      "assetid": "0",
      "amount": "1",
      "txtype": "swap",
      "tx": "not set"
    }
  ]
}

```

**Example:**

```bash
curl -X POST -H "Content-Type: application/json" -d '{"id": "H!Xz6LWg"}' http://localhost:8081/scenario/tx
```
* * *

### 11\. Get Scenario Info

**Endpoint:** `/scenario/info`

**Method:** `POST`

**Description:**
Retrieves detailed information about a specific scenario.

**Request Body:**

```json
{
  "id": "<scenario_id>"
}
```

**Response:**

```json
{
  "success": true,
  "result": [
    {
      "source_chain": "polkadot",
      "source_address": "5GdvmQtUwByTt6Vkx41vtWvg5guyaH3BL2yn6iamg1RViiKD",
      "dest_chain": "assetHub",
      "dest_address": "5D7RT7vqgZKUoKxrPMihNeXBzhrmWjd5meprfUFhtrULJ4ng",
      "assetid": "0",
      "amount": "1",
      "txtype": "swap",
      "tx": "not set"
    }
  ]
}
```

**Example:**

```bash
curl -X POST -H "Content-Type: application/json" -d '{"id": "H!Xz6LWg"}' http://localhost:8081/scenario/info
```

* * *

### 12\. List Active All Workers

**Endpoint:** `/scenario/all_workers`

**Method:** `GET`

**Description:**
Lists all active scenario workers.

**Response:**

-   **Body:** A JSON array of active threads.

**Example:**

```bash
curl -X GET http://localhost:8081/scenario/all_workers
```
* * *

### 13\. Get Worker Logs

**Endpoint:** `/scenario/worker/logs`

**Method:** `POST`

**Description:**
Retrieves execution logs for a specific scenario worker.

**Request Body:**

```json
{
  "id": "<scenario_id>"
}
```

**Response:**

```json
{
  "success": true,
  "result": [
    "Log entry 1",
    "Log entry 2"
  ]
}
```

**Example:**

```bash
curl -X POST -H "Content-Type: application/json" -d '{"id": "H!Xz6LWg"}' http://localhost:8081/scenario/worker/logs
```
* * *

### 14\. Dry Run HTTP Action

**Endpoint:** `/action/http/dry_run`

**Method:** `POST`

**Description:**
Tests an HTTP action.
_Currently a placeholder implementation._

**Response:**

```json
{
  "success": false,
  "result": "not found"
}
```

**Example:**

```bash
curl -X POST http://localhost:8081/action/http/dry_run
```
* * *

