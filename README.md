# German Cities Project - Web Scraping, APIs, and MySQL

A small data pipeline that collects information about three German 
cities - Berlin, Hamburg, and Munich - from multiple sources, and 
stores it in a relational MySQL database.

## What this project does

- **Web scraping**: pulls country, coordinates, and population for 
  each city from Wikipedia
- **OpenWeather API**: fetches a 5-day weather forecast for each city
- **AeroDataBox API** (via RapidAPI): finds each city's major airport 
  and pulls tomorrow's flight arrivals

All of this is loaded into a MySQL database with five related tables, 
linked through a shared `city_id`:

- `cities` - static reference data (name, country, coordinates)
- `populations` - population figures over time
- `forecasts` - weather forecast data
- `airports` - each city's major airport
- `arrivals` - flight arrivals linked to each city's airport

The notebook is built so it can be re-run from top to bottom at any 
time without creating duplicate data - every table is dropped and 
rebuilt fresh on each run.

## Tech stack

- Python (requests, BeautifulSoup, pandas)
- MySQL (via SQLAlchemy + PyMySQL)
- OpenWeatherMap API
- AeroDataBox API (via RapidAPI)

## Setup

1. Clone this repository
2. Install the required packages:
   `pip install requests beautifulsoup4 pandas python-dotenv pymysql sqlalchemy`
3. Create a MySQL database (e.g. `sql_workshop`)
4. Copy `.env.example` to a new file named `.env`, and fill in your 
   own credentials and API keys:

DB_HOST=127.0.0.1
DB_USER=root
DB_PASSWORD=your_password_here
DB_PORT=3306
DB_SCHEMA=sql_workshop
OPENWEATHER_API_KEY=your_api_key_here
RAPIDAPI_KEY=your_api_key_here

5. Open `WebScraping_to_SQL.ipynb` in Jupyter, and run all cells from 
   top to bottom

## Notes

- API keys and database credentials are never stored in the notebook 
  itself - only in `.env`, which is excluded from version control via 
  `.gitignore`
- Flight arrival data is pulled for "tomorrow" relative to whenever 
  the notebook is run, so results will differ each day