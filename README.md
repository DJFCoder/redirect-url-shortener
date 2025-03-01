# URL Shortener Redirect API

## Overview

This project implements a serverless API for URL shortening using AWS Lambda and S3. It allows redirecting users from short URLs to the original URLs, with support for link expiration.

## Features

- Redirection from short URLs to original URLs
- URL expiration verification
- Data storage in S3 bucket
- Response with appropriate HTTP status codes

## Architecture

The application consists of:

1. **AWS Lambda Function**: Processes HTTP requests and performs the redirection
2. **Amazon S3**: Stores the mapping data between short URLs and original ones
3. **Data Model**: Representation of URL data with expiration time

## How It Works

1. User accesses a short URL (e.g., `https://yourdomain.com/abc123`)
2. The Lambda function is invoked and extracts the short URL code from the request path
3. The function fetches the corresponding JSON file from the S3 bucket (`abc123.json`)
4. If the file is found, the function verifies if the URL has expired
5. If the URL is valid, the API returns an HTTP 302 redirect to the original URL
6. If the URL has expired, the API returns an HTTP 410 status (Gone)

## File Structure

- `Main.java`: Main class that implements the Lambda function handler
- `UrlData.java`: Model class for URL data

## Storage Format

Data is stored in S3 as JSON files with the following format:

```json
{
    "originalUrl": "https://full-original-url.com/path",
    "expirationTime": 1640995200
}
```

Where `expirationTime` is the Unix timestamp (in seconds) that defines when the URL expires.

## Technologies Used

- Java
- AWS Lambda
- Amazon S3
- Jackson (for JSON processing)
- Lombok (for boilerplate reduction)
- AWS SDK for Java v2

## Requirements

- JDK 11 or higher
- Maven
- AWS CLI configured with appropriate credentials
- S3 bucket configured for data storage

## Configuration

To use this application, you need to:

1. Create an S3 bucket named `url-shortener-devjf` (or change the name in the code)
2. Configure Lambda to be triggered by HTTP requests via API Gateway
3. Set up the necessary permissions for Lambda to access the S3 bucket

## Limitations

- Does not include the functionality to create short URLs (only redirection)
- Does not include authentication or authorization mechanisms
- Does not have access metrics or analytics system
