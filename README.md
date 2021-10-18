## Event aggregator

Event aggregator is a simple server service. It should be written in **Golang** or **Node** and run with the newest version.
Try to use only standard libraries and implement all data handling in memory.
The service should be able to capture incoming *events* and provide aggregated data. 
Therefor, there should be 2 main endpoints for the service:
```
- GET /:name?from=date&to=date&interval=minutes     - gets aggregated data
- POST /:name                                       - creates new event
```

### Events

Every event is defined by it's name. Server should be able to save these events and group them by their name.
Every event should be associated with the time of its arrival.
### Aggregations

Users requesting the GET endpoint should be able to get aggregated data from the server. Aggregations are limited by two dates.
Interval must also be set for every aggregation. The interval is set in minutes. 
Consider that there will be significantly more write requests then read operations.

### Examples

**Event**

```
POST /click
```

**Aggregation**

Request:
```
from=1478116800 (Human time (GMT): Wed, 02 Nov 2016 20:00:00 GMT)
to=1478120400 (Human time (GMT): Wed, 02 Nov 2016 21:00:00 GMT)
interval=10 (10 minutes)
```

That means the raw request will be:
```
GET /click?from=1478116800&to=1478120400&interval=10
```

Response:
```
[
  { click: 100 }, // first 10 minutes
  { click: 200 }, // 10-20 minutes
  { click: 300 }, // ...
  { click: 200 },
  { click: 100 },
  { click: 100 }
]
```

### Bonus
Implement a test validating listing functionality, when 5 **concurrent** users are sending events to the service.
