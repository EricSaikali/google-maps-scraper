# Google Maps Scraper API

A FastAPI service for scraping Google Maps data based on search queries. Ideal for n8n users.

Very high performance, watch out for rate limiting!

Use variables to replace URL parameters

scrape-get?query=hotels%20in%2098392&max_places=100&lang=en&headless=true"

If using n8n or other automation, use the /scrape-get endpoint for it to return results

simple install, copy files and run docker compose up -d

Intened to be used with this n8n build: 
https://github.com/conor-is-my-name/n8n-autoscaling 

## API Endpoints

**Parameters:**
- `query` (required): Search query (e.g., "hotels in 98392")
- `max_places` (optional): Maximum number of results to return
- `lang` (optional, default "en"): Language code for results
- `headless` (optional, default true): Run browser in headless mode

### GET `/scrape-get`
Alternative GET endpoint with same functionality

### GET `/`
Health check endpoint

## Example Requests

### GET Example
```bash
curl -X GET "http://localhost:8001/scrape" \
-H "Content-Type: application/json" \
-d '{
  "query": "hotels in 98392",
  "max_places": 10,
  "lang": "en",
  "headless": true
}'
```

### GET Example
```bash
curl "http://localhost:8001/scrape-get?query=hotels%20in%2098392&max_places=10&lang=en&headless=true"
```
or

```bash
curl "http://gmaps_scraper_api_service:8001/scrape-get?query=hotels%20in%2098392&max_places=10&lang=en&headless=true"
```


## Running the Service

### Docker
```bash
docker-compose up --build
```

### Local Development
1. Install dependencies:
```bash
pip install -r requirements.txt
```

2. Run the API:
```bash
uvicorn gmaps_scraper_server.main_api:app --reload
```


The API will be available at `http://localhost:8001`

or for docker:

`http://gmaps_scraper_api_service:8001`

## Notes
- For production use, consider adding authentication
- The scraping process may take several seconds to minutes depending on the number of results
- Results format depends on the underlying scraper implementation
