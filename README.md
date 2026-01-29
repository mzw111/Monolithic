# CC Lab 2 - Monolithic App
SRN: PES1UG23CS365

## Setup

Install dependencies:
```
pip install -r requirements.txt
```

Add events to database:
```
python insert_events.py
```

Run server:
```
python -m uvicorn main:app --reload
```

Server runs at http://localhost:8000

## Load Testing

```
locust -f locust/checkout_locustfile.py
locust -f locust/events_locustfile.py
locust -f locust/myevents_locustfile.py
```

Locust UI: http://localhost:8089

## What I Did

Fixed performance issues in three routes by removing unnecessary loops.

**/events route**
- Had 3 million iterations doing nothing
- Removed the loop, response time dropped from 242ms to under 50ms

**/my-events route**  
- Had 1.5 million iterations incrementing a dummy variable
- Removed it, got similar improvement

**/checkout route**
- Used while loops to sum fees instead of direct addition
- Changed to simple sum, much faster now

The crash bug (division by zero) was there to show how one error breaks the whole app in monolithic architecture.
