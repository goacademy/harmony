# Overview

harmony is a go library that orchestrates complex workflow to ensure a state of consistency.

Developers often need to write complex business logic that require succesful execution of multiple methods.
For example, an ecomerce website requires a number of API calls and database operations. Such method is usually written as something like this:

- Unmarshal data
- Call API Endpoint 1
- Handle Error
- Call API Endpoint 2
- Handle Error
- Update Database Record
- Handle Error
- Return Success

The challenge is that every call could fail which lead to inconsistent state across distributed systems. These failures can be monitored through logs or application metrics, but in case of failures from external systems such as an external integration partner is down, recovering those failure requires siginicant manual effort.

Harmony was developed to address this issue by converting a single business process which does many things to a number of independent processes orchestrated by a workflow.

For example, the same logic above is converted into:

Process 1 - Unmarshal Data, Call API Endpoint 1

Process 2 - Call API Endpoint 2

Process 3 - Update Database Record, return success

Between every 2 processes, a default retry protocol is applied. Optionally, failed processes can be rescheduled or aborted with a callback.
