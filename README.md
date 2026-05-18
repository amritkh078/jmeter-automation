# Part B — API Testing (JMeter)

API: `https://dummyjson.com`

## Run (one command)

```bash
rm -rf ./output/html-report ./output/results.jtl && \
jmeter -n \
  -t PartB_API_Testing.jmx \
  -l ./output/results.jtl \
  -JcsvFilePath=./test_products.csv \
  -JoutputDir=./output \
  -e -o ./output/html-report
```

- **HTML report** → `output/html-report/index.html`
- **Transformed JSON** → `output/users_transformed.json`

## View HTML Report

```bash
open ./output/html-report/index.html
```

## What the tests do

| Task | Request | Assertions |
|------|---------|------------|
| Task 2 | `POST /products/add` × 5 (one per CSV row) | HTTP 201, `id` field exists, title/category/price match CSV, response time < 5s |
| Task 3 | `GET /users` × 1 | HTTP 200, `users` array exists, ≥ 10 users, response time < 5s |

Task 3 Groovy script processes the first 10 users, calculates average age, gender and department distribution, and saves the result to `output/users_transformed.json`.

## Requirements

- Java 11+
- Apache JMeter 5.6+ (`brew install jmeter` on Mac)
