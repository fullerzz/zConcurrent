![CI Workflow](https://github.com/fullerzz/zConcurrent/actions/workflows/ci.yml/badge.svg)
[![Ruff](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/astral-sh/ruff/main/assets/badge/v2.json)](https://github.com/astral-sh/ruff)
[![Poetry](https://img.shields.io/endpoint?url=https://python-poetry.org/badge/v0.json)](https://python-poetry.org/)

# Overview

This project allows you to execute a list of http operations asynchronously from within an synchronous context.

It does not care whether you should do this. It simply allows you to do so if you so desire.

## Installing

The package is available via pip. (Soon)

```bash
pip install zconcurrent
```

## Usage

The package can be imported as shown:

```python
from zconcurrent.zsession import zSession, RequestMap, RequestResults
```

| Class | Description|
| ----- | -----------|
| `zSession` | Session object containing collection of requests to send |
| `RequestMap` | Container object that stores all info about an individual request to send |
| `RequestResults` | Container object that stores the request responses and any exceptions raised |


### Example

```python
req1 = RequestMap(url="https://baconipsum.com/api", httpOperation="GET", queryParams={"type": "meat-and-filler", "format": "json"})
req2 = RequestMap(url="https://baconipsum.com/api", httpOperation="GET", queryParams={"type": "all-meat", "format": "json"})
req3 = RequestMap(url="https://baconipsum.com/api", httpOperation="GET", queryParams={"type": "meat-and-filler", "format": "json"})

session = zSession(requestMaps=[req1, req2, req3])
reqResps: RequestResults = mySession.sendRequests()
```

### RequestResults Class

```python
@dataclass
class RequestResults:
    requestResponses: list[RequestResponse]
    taskExceptions: list[BaseException]
```
