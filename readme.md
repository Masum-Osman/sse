# Go SSE Server

This project demonstrates a simple **Server-Sent Events (SSE)** implementation in Go. It allows the server to send real-time updates to connected clients. This example uses basic **CORS** configuration to allow cross-origin requests.

## Features
- Real-time updates using Server-Sent Events (SSE)
- Basic CORS support for cross-origin requests
- Customizable data sent in SSE messages

## Requirements
- Go 1.20 or later
- Internet connection for downloading dependencies (if needed)

## How to Run

### 1. Clone the repository

```bash
git clone https://github.com/Masum-Osman/sse.git
cd sse
```

### 2. Install Dependencies

This project uses Go’s built-in libraries, so no additional dependencies are required.

### 3. Run the Go Server

Start the server by running the following command:

```bash
go run main.go
```

By default, the server will start on `http://localhost:8000`.

### 4. Test the SSE Endpoint

To test the server using **cURL**, use the following command in your terminal:

```bash
curl 'http://localhost:8000/events' \
  -H 'Accept: text/event-stream' \
  -H 'Accept-Language: en-GB,en-US;q=0.9,en;q=0.8' \
  -H 'Cache-Control: no-cache' \
  -H 'Connection: keep-alive' \
  -H 'Origin: null' \
  -H 'Sec-Fetch-Dest: empty' \
  -H 'Sec-Fetch-Mode: cors' \
  -H 'Sec-Fetch-Site: cross-site' \
  -H 'User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36' \
  -H 'sec-ch-ua: "Google Chrome";v="131", "Chromium";v="131", "Not_A Brand";v="24"' \
  -H 'sec-ch-ua-mobile: ?0' \
  -H 'sec-ch-ua-platform: "macOS"'
```

This cURL command will initiate a request to the `/events` endpoint and print the real-time updates sent by the server.

### 5. Client-Side Example

Here’s how you can implement SSE on the client side using JavaScript.

```javascript
const eventSource = new EventSource('http://localhost:8000/events');

// Listen for messages from the server
eventSource.onmessage = function(event) {
    console.log('New event:', event.data);
};

// Error handling
eventSource.onerror = function(error) {
    console.error('Error occurred:', error);
};
```

This script will listen for events sent by the server and log them to the browser's console.

### 6. CORS Configuration

The Go server is configured to handle **CORS** (Cross-Origin Resource Sharing) to allow client-side applications from different origins to make requests to the SSE endpoint. The server adds the following headers:

- `Access-Control-Allow-Origin: *` (allows all origins or specific origins for more security)
- `Access-Control-Allow-Methods: GET, POST`
- `Access-Control-Allow-Headers: Content-Type`

### Troubleshooting

- If you receive CORS-related errors, ensure your server is configured with the correct headers.
- Make sure your Go server is running and accessible at the specified port.
- If you experience a **connection refused** error, ensure that the server is correctly listening on the right port (`8080` in this example).
