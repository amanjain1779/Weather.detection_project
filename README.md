# Weather.detection_project
# Real time Weather detection system using API :

import requests
import sys

def get_weather(api_key,city):
  url = f"http://api.openweathermap.org/data/2.5/weather?q={city}&appid={api_key}&units=metric"

   try:
        response = requests.get(url)
        response.raise_for_status()
        return response.json()
    
  except requests.exceptions.HTTPError as http_error:
        print(f"HTTP error occured :{http_error}")

  except requests.exceptions as error:
        print(f"error detected: {error}")

def display_weather(data):
    if data:
        city = data['name']
        country = data['sys']['country']
        temp = data['main']['temp']
        description = data['weather'][0]['description']
        print(f"weather in {city} , {country}:")
        print(f"tempreature : {temp}°C")
        print(f"condition : {description.capitalize()}")

def main():
    if len(sys.argv) != 2:
        print("usage : python weather.py <city>")
        sys.exit(1)

city = sys.argv[1]
api_key = "973ff9ba8403cbca85443103f9fac011"
weather_data = get_weather(api_key,city)
display_weather(weather_data)

if __name__ == "__main__":
    main()


