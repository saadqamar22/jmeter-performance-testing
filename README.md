# JMeter Performance Testing

Performance testing a public REST API using Apache JMeter, covering load testing, timers, assertions, listeners, and correlation using Regular Expression Extractor.

## Target API
JSONPlaceholder — https://jsonplaceholder.typicode.com

## Tasks Covered

| Task | Description |
|------|-------------|
| Task 1 | Basic test plan — single user execution |
| Task 2 | Multiple users (5) with multiple listener formats |
| Task 3A | Constant Timer (1000ms delay) |
| Task 3B | Uniform Random Timer (1000ms offset, 5000ms max) |
| Task 4 | Correlation using Regular Expression Extractor |
| Task 5 | Correlation with multiple listener formats |
| Task 6 | Response and Duration Assertions |
| Extension | Load test — 50 concurrent users |

## Results Summary

The current generated report is available in `results/html-report/index.html`.

### Current run highlights
- Total samples: 87
- Average response time: 412ms
- Min response time: 110ms
- Max response time: 1423ms
- Throughput: 8.15 req/sec
- Error rate: 8.05%

### HTTP Request sampler summary
- Sample count: 66
- Average response time: 411ms
- Min response time: 110ms
- Max response time: 1423ms
- Throughput: 6.18 req/sec
- Error rate: 0.00%

### Correlation results
- POST `/posts` creates a resource and extracts `id` using regex `"id":\s*(\d+)`
- GET `/posts/${postId}` uses the extracted value dynamically
- Result: the GET request returns 100% errors in this run because JSONPlaceholder does not persist POSTed data, so the generated ID is valid but the resource is not retained.

### Assertions
- Response Code = 200
- Response Time < 2000ms

## Folder Structure

jmeter-performance-testing/
├── testplans/
│   └── JMeter Performance Testing - JSONPlaceholder.jmx
├── results/
│   ├── html-report/
│   │   └── index.html
│   └── results.jtl
└── README.md

## How to Run

Open `testplans/JMeter Performance Testing - JSONPlaceholder.jmx` in Apache JMeter and click the Play button.

Or run in non-GUI mode from the JMeter `bin` directory:

```bash
./jmeter -n -t ~/Desktop/jmeter-performance-testing/testplans/JMeter\ Performance\ Testing\ -\ JSONPlaceholder.jmx \
  -l ~/Desktop/jmeter-performance-testing/results/results.jtl \
  -e -o ~/Desktop/jmeter-performance-testing/results/html-report
```

Then open the report:

```bash
open ~/Desktop/jmeter-performance-testing/results/html-report/index.html
```
