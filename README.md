# 🌦️ Weather App - Django

**Last Updated:** 1 Nov 2025

This project is a **Django-based Weather App** that allows users to
search for any city and view its current weather details, including:

-   🌡️ Temperature
-   💧 Humidity
-   📊 Pressure
-   ☁️ Weather conditions

The application fetches **live weather data** from the **OpenWeatherMap
API** and displays it through a simple and user-friendly interface.

Additionally, the application stores the **last 5 recent searches** so
users can quickly view recently searched cities along with their weather
information.

This project demonstrates:

-   Django project and app structure
-   Integration with external APIs
-   Using Django models for data storage
-   Dynamic template rendering
-   Handling HTTP requests in Django

------------------------------------------------------------------------

# 📌 Features

-   Search weather by **city name**
-   Display **real-time weather data**
-   Show **weather icon**
-   Store **search history**
-   Display **last 5 searched cities**
-   Simple and clean UI

------------------------------------------------------------------------

# 🛠️ Tech Stack

-   Python
-   Django
-   HTML
-   CSS
-   OpenWeatherMap API
-   SQLite (default Django database)

------------------------------------------------------------------------

# 📂 Project Structure

    weather/
    │
    ├── weather/
    │   ├── settings.py
    │   ├── urls.py
    │
    ├── main/
    │   ├── models.py
    │   ├── views.py
    │   ├── urls.py
    │   └── templates/
    │       └── main/
    │           └── index.html
    │
    ├── manage.py

------------------------------------------------------------------------

# ⚙️ Installation

### 1️⃣ Clone the Repository

``` bash
git clone https://github.com/yourusername/django-weather-app.git
cd django-weather-app
```

### 2️⃣ Create Virtual Environment

``` bash
python -m venv venv
```

Activate environment

**Windows**

``` bash
venv\Scripts\activate
```

**Mac / Linux**

``` bash
source venv/bin/activate
```

### 3️⃣ Install Dependencies

``` bash
pip install django requests
```

### 4️⃣ Run Database Migrations

``` bash
python manage.py makemigrations
python manage.py migrate
```

------------------------------------------------------------------------

# 🔑 OpenWeatherMap API Setup

1.  Create an account at:

https://openweathermap.org/api

2.  Generate your **API Key**

3.  Replace the API key in `views.py`

``` python
API_KEY = "your_api_key_here"
```

------------------------------------------------------------------------

# 🗄️ Database Model

``` python
class SearchHistory(models.Model):
    city_name = models.CharField(max_length=100)
    temperature = models.FloatField(null=True, blank=True)
    humidity = models.IntegerField(null=True, blank=True)
    pressure = models.IntegerField(null=True, blank=True)
    description = models.CharField(max_length=255, null=True, blank=True)
    searched_at = models.DateTimeField(auto_now_add=True)
```

This model stores:

-   City name
-   Temperature
-   Humidity
-   Pressure
-   Weather description
-   Timestamp of search

------------------------------------------------------------------------

# 🌐 URL Configuration

### Project URLs

`weather/urls.py`

``` python
urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('main.urls')),
]
```

### App URLs

`main/urls.py`

``` python
urlpatterns = [
    path('', views.index),
]
```

------------------------------------------------------------------------

# 🧠 View Logic

The main logic is handled inside the `index()` view.

Responsibilities:

-   Handle GET and POST requests
-   Call OpenWeatherMap API
-   Parse JSON response
-   Save search results to database
-   Retrieve last 5 searches

Example:

``` python
resp = requests.get(url, timeout=5)
data = resp.json()
```

Recent searches:

``` python
SearchHistory.objects.order_by('-searched_at')[:5]
```

------------------------------------------------------------------------

# 🎨 Template

Location:

    main/templates/main/index.html

Features:

-   Search form
-   Weather information display
-   Weather icon
-   Recent search list
-   Simple inline CSS

Example icon:

``` html
<img src="https://openweathermap.org/img/wn/{{ weather.icon }}@2x.png">
```

------------------------------------------------------------------------

# ▶️ Running the Project

Start the server:

``` bash
python manage.py runserver
```

Open browser:

    http://127.0.0.1:8000

------------------------------------------------------------------------

# 🚀 Possible Improvements

-   Add Bootstrap or Tailwind UI
-   Add city autocomplete
-   Cache API responses
-   Add search history page
-   Add 5‑day forecast
-   Add user authentication

------------------------------------------------------------------------

# 📄 License

This project is open-source and available under the **MIT License**.

------------------------------------------------------------------------

# 👨‍💻 Author

Created as a **Django learning project** demonstrating:

-   API integration
-   Django models
-   Template rendering
-   Full web application workflow
