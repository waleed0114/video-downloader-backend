# Video Downloader Backend

A Node.js backend service for video downloading functionality.

## Prerequisites

- Node.js (v14 or higher)
- npm (v6 or higher)

## Setup

1. Install dependencies:
```bash
npm install
```

2. Create a `.env` file in the root directory with the following variables:
```
PORT=3001
NODE_ENV=development
CORS_ORIGIN=http://localhost:3000
TWITTER_BEARER_TOKEN=your_twitter_bearer_token  # Optional: For enhanced API access
INSTAGRAM_COOKIE=your_instagram_cookie  # Optional: For enhanced Instagram access
```

3. Start the development server:
```bash
npm run dev
```

4. For production:
```bash
npm start
```

## API Endpoints

### Test Route
- **GET** `/test`
- Returns: `{ status: "Backend Running" }`

### Facebook Video Download
- **POST** `/api/facebook/download`
- Request body:
  ```json
  {
    "url": "https://www.facebook.com/video/url"
  }
  ```
- Success response:
  ```json
  {
    "status": "success",
    "data": {
      "title": "Video Title",
      "thumbnail": "thumbnail_url",
      "downloadUrl": "direct_video_url",
      "platform": "facebook",
      "timestamp": "2024-03-14T12:00:00.000Z"
    }
  }
  ```

### Twitter Video Download
- **POST** `/api/x/download`
- Request body:
  ```json
  {
    "url": "https://twitter.com/username/status/123456789"
  }
  ```
- Success response:
  ```json
  {
    "status": "success",
    "data": {
      "title": "Tweet Title",
      "thumbnail": "thumbnail_url",
      "variants": [
        {
          "url": "video_url",
          "quality": "720p",
          "width": 1280,
          "height": 720
        },
        {
          "url": "video_url",
          "quality": "480p",
          "width": 854,
          "height": 480
        }
      ],
      "platform": "twitter",
      "timestamp": "2024-03-14T12:00:00.000Z"
    }
  }
  ```

### Instagram Video Download
- **POST** `/api/instagram/download`
- Request body:
  ```json
  {
    "url": "https://www.instagram.com/p/ABC123xyz/"
  }
  ```
- Success response:
  ```json
  {
    "status": "success",
    "data": {
      "title": "Post Caption",
      "thumbnail": "thumbnail_url",
      "downloadUrl": "video_url",
      "duration": 30,
      "width": 1080,
      "height": 1920,
      "platform": "instagram",
      "timestamp": "2024-03-14T12:00:00.000Z"
    }
  }
  ```

### Error Responses
- 400: Invalid URL
- 403: Private content
- 404: Content not found
- 429: Rate limit exceeded
- 500: Server error
- 503: Network error

## Environment Variables

- `PORT`: Server port (default: 3001)
- `NODE_ENV`: Environment mode (development/production)
- `CORS_ORIGIN`: Allowed origin for CORS (default: http://localhost:3000)
- `TWITTER_BEARER_TOKEN`: Twitter API bearer token (optional)
- `INSTAGRAM_COOKIE`: Instagram session cookie (optional)

## Development

The project uses:
- Express.js for the server
- CORS for handling cross-origin requests
- dotenv for environment variables
- nodemon for development auto-reload
- axios for HTTP requests

## License

ISC 