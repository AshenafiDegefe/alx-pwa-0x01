## API Overview:
The MoviesDatabase API provides comprehensive access to a vast and up-to-date database of movies, TV shows, and celebrity information. Its **key features** include:
* **Extensive Catalog:** Access to a massive library of titles, including current box office hits, classics, and independent films.
* **Detailed Metadata:** Retrieval of rich movie data such as plot summaries, genre classifications, release dates, and user ratings.
* **Search Functionality:** Robust searching capabilities for titles, cast, and crew.
* **Image and Poster Assets:** Links to high-resolution posters, backdrops, and cast photos.
* **Discover Endpoints:** Specialized endpoints to find trending, top-rated, or recently released content.

  ## API Version
This documentation is based on **Version 3 (v3)** of the MoviesDatabase API.

## Available Endpoints

The API is structured around RESTful principles. Here is a list of the primary endpoints:

| Endpoint Path | Description |
| :--- | :--- |
| `/titles/search` | Searches the database for movies or TV shows based on a query string. |
| `/titles/{id}` | Retrieves all detailed information for a specific title using its unique ID. |
| `/titles/trending` | Fetches a list of the currently trending movies and TV shows. |
| `/people/search` | Searches for actors, directors, or other crew members. |
| `/genres` | Lists all available movie genres for filtering or categorization. |
| `/images/{id}` | Retrieves image assets (posters, backdrops) for a specific title. |

## Request and Response Format
All API communication is conducted over **HTTPS**.

### Request Format

Requests are typically **GET** requests. Parameters are passed as **query parameters** in the URL.

**Example Request:**
To search for the movie 'Inception':
GET https://api.moviesdatabase.com/v3/titles/search?q=Inception&limit=10

### Response Format

All successful responses are returned as a JSON object with a consistent structure.

**Example Successful Response Object (`/titles/{id}`):**

```json
{
  "status": "success",
  "data": {
    "id": "tt1375666",
    "title": "Inception",
    "release_date": "2010-07-16",
    "runtime_minutes": 148,
    "genres": ["Action", "Sci-Fi", "Thriller"],
    "rating": 8.8,
    "plot_summary": "A thief who steals corporate secrets through the use of dream-sharing technology...",
    "cast": [
      {"name": "Leonardo DiCaprio", "role": "Cobb"},
      // ... more cast
    ]
  }
}

## Authentication
The MoviesDatabase API uses an API Key for authentication.
Requirement
Your API key must be included in every request either as a query parameter or via a dedicated HTTP header.

1. Recommended Method (Header): Pass your unique API key in the Authorization header with the Bearer scheme:
Header Name,Value
Authorization,Bearer YOUR_API_KEY_HERE
2. Alternative Method (Query Parameter): Include the key as a query parameter named api_key:
GET [https://api.moviesdatabase.com/v3/titles/search?q=query&api_key=YOUR_API_KEY_HERE](https://api.moviesdatabase.com/v3/titles/search?q=query&api_key=YOUR_API_KEY_HERE)
Note: Always keep your API key secure. Do not expose it in client-side code or public repositories.

## Error Handling
The API uses standard HTTP status codes to indicate the success or failure of a request. The response body for errors is a JSON object that includes an error message and code.
Handling Errors:

It is essential to check the HTTP status code first. If the status is not 200, parse the JSON error body to retrieve the code and message to provide meaningful feedback to the user or log the issue for debugging.

## Usage Limits and Best Practices
### Usage Limits (Rate Limiting)
The API enforces a rate limit to ensure fair usage and maintain service stability.

Free Tier: 100 requests per minute (RPM).

Requests that exceed the limit will receive a 429 Too Many Requests status code.
### Best Practices
Cache Responses: Store API responses locally (e.g., in a database or temporary cache) for frequently accessed data (like popular movie lists or genres) to reduce the number of requests and improve application performance.

Use Specific Endpoints: When possible, use specific endpoints (e.g., /titles/{id}) instead of broad searches to minimize data transfer and ensure accuracy.

Handle 429 Errors: Implement backoff and retry logic to gracefully handle 429 responses. Do not immediately retry failed requests; wait for the time specified in the Retry-After header (if available) or implement an exponential delay.

Secure API Key: Load your API key from environment variables (e.g., .env file) and ensure it is never committed directly to source control.
