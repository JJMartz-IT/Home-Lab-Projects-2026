# Weather CLI

A simple command-line tool that looks up the current weather for any city, written in Python. Built as a project to learn how to work with web APIs.

### What it does
Takes a city name as input (e.g. Lancaster, US)
Resolves it to coordinates using Open-Meteo's free geocoding API
Fetches the current temperature and wind speed for that location
Handles unmatched cities and network errors without crashing

### Example
Enter a city (or 'quit' to exit): Lancaster, US
It's 74.1°F in Lancaster, with wind at 6.2 mph.

Enter a city (or 'quit' to exit): Nowhereville
Couldn't find that city. Try including a state or country, e.g. 'Lancaster, US'.

Enter a city (or 'quit' to exit): quit

### Installation
[git clone](Weather CLI Tool Code)
cd weather-cli
python -m venv venv
source venv/bin/activate      # Windows: venv\Scripts\activate
pip install -r requirements.txt

### Usage
python weather.py

Enter any city name when prompted (adding a state or country, e.g. "Paris, France", helps disambiguate common city names). Type quit to exit.

### How it works

The tool calls two separate Open-Meteo endpoints:

Geocoding API — turns a city name into latitude/longitude, since the forecast API needs coordinates rather than a name.
Forecast API — returns the current temperature and wind speed for those coordinates.

No API key or sign-up is required for either endpoint.

### What I learned
How to call a REST API from Python using requests
Reading and pulling specific values out of nested JSON responses
Composing small functions together (get_coordinates() feeding into get_weather())
Basic error handling with try/except and raise_for_status()

### Built with
Python 3
Requests
Open-Meteo API
