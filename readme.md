In this tutorial, we are going to retrieve the weather forecast of any place using Python programming. We will be using the API call approach in this code snippet. To finish this task we will be importing the requests module, this module allows us to send HTTP requests using Python. In this, we will be expecting a JSON format response of our API call. We will be using the OpenWeatherMap API to get our weather forecast, we can also use other weather APIs like AerisWeather, ClimaCell, DarkSky etc.

Developing a Weather forecasting script in Python
First, let us begin by importing the requests package.
```
import requests
```
Now let us initialize our API key and base_url variables.

To get your API key, click here. Sign up and then subscribe to current weather data.
```
api_key = "Enter your API key here"
url= "http://api.openweathermap.org/data/2.5/weather?"
```
Here base_url is the URL to interact with the API, read the documentation here. Now we can get the forecast for our place by adding or appending queries to the base_url.

Now let us take the input, add the query to our base_url and make an API request to the server.
```
city_name = input("Enter city name : ") 
full_url = url+ "q=" + city_name + "&appid=" + api_key
req= requests.get(full_url)
info = req.json()
```
We converted the response to JSON format. This is how the response looks.
```
{'coord': {'lon': 78.47, 'lat': 17.38}, 'weather': [{'id': 802, 'main': 'Clouds', 'description': 'scattered clouds', 'icon': '03n'}], 'base': 'stations', 'main': {'temp': 299.07, 'feels_like': 301.84, 'temp_min': 298.15, 'temp_max': 299.82, 'pressure': 1012, 'humidity': 78}, 'visibility': 6000, 'wind': {'speed': 2.6, 'deg': 240}, 'clouds': {'all': 40}, 'dt': 1595780101, 'sys': {'type': 1, 'id': 9214, 'country': 'IN', 'sunrise': 1595723010, 'sunset': 1595769690}, 'timezone': 19800, 'id': 1269843, 'name': 'Hyderabad', 'cod': 200}
```
Now let us filter out the useful information like the current temperature, pressure, humidity, description and wind speed.
```
if info["cod"] != "404": 
    x = info["main"] 
    current_temperature = x["temp"]
    tnc = round(float(current_temperature - 273.15),2)
    current_pressure = x["pressure"] 
    current_humidiy = x["humidity"] 
    z = info["weather"] 
    weather_description = z[0]["description"]
    s = info["wind"]
    speed = s["speed"]
    print()
    print("Temperature (in celsius unit): ",  round(float(current_temperature - 273.15),2) , "°C",
            "\nAtmospheric pressure : " + str(current_pressure) + "hpa"
            "\nHumidity : " + str(current_humidiy) + "%"
            "\nDescription: " + str(weather_description).capitalize()+
                "\nWind Speed :" + str(speed) + "m/s")
else: 
  print(" City Not Found ")

```
Python dictionary operations are used to retrieve the data from the JSON format.

Notice that in line 12, we are performing a quick Kelvin to Celsius conversion.

Yay! Our script is now ready to implement.

Output1:
```
Enter city name: Hyderabad

Temperature (in celsius unit):  25.92 °C 
Atmospheric pressure : 1012hpa
Humidity : 78%
Description: Scattered clouds
Wind Speed :2.6m/s
```
Output2:
```
Enter city name: Winterfell

City Not Found
```
Full Program:

```
import requests
api_key = "#Enter your API key here"
url= "http://api.openweathermap.org/data/2.5/weather?"
city_name = input("Enter city name : ") 
full_url = base_url + "q=" + city_name + "&appid=" + api_key
req = requests.get(full_url)
info = req.json() 
if info["cod"] != "404": 
    x = info["main"] 
    current_temperature = x["temp"]
    tnc = round(float(current_temperature - 273.15),2)
    current_pressure = x["pressure"] 
    current_humidiy = x["humidity"] 
    z = info["weather"] 
    weather_description = z[0]["description"]
    s = info["wind"]
    speed = s["speed"]
    print()
    print("Temperature (in celsius unit): ", 
                  round(float(current_temperature - 273.15),2) , "°C",
            "\nAtmospheric pressure : " +
                  str(current_pressure) + "hpa"
            "\nHumidity : " +
                  str(current_humidiy) + "%"
            "\nDescription: " +
                  str(weather_description).capitalize()+
                "\nWind Speed :" + str(speed) + "m/s")
else: 
  print(" City Not Found ")

```