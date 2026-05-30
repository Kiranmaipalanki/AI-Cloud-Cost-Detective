## Prompt 1: FastAPI Backend + AWS SDK (Boto3)

Create a Python FastAPI backend in a `backend/` folder for the AI Cloud Cost Detective project.

## What to build

-A FastAPI server with a `POST /api/analyze` endpoint that accepts `{ "region": "<name>" }`.
-A `GET /api/regions` endpoint that returns the list of AWS regions.
-Use Python's `boto3` SDK to interact with AWS:
`boto3.client('ec2').describe_regions()` to list all available regions.
`boto3 service clients` to fetch all resources in the selected region.
-Parse the Boto3 JSON responses and return a structured response with resource type, name, location, SKU, and tags.
-Add error handling for AWS credentials not configured, invalid credentials, or invalid region.
-Enable CORS for `http://localhost:5173`.
-Include a `requirements.txt` with `fastapi`, `uvicorn`, `boto3`.

## Project structure
```
backend/
├── main.py
├── aws_scanner.py
├── requirements.txt
```
Refer to `Architecture.MD` and `RequestFlow.MD`. This covers step ③ of the request flow.
