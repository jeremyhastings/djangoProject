# Django Project

## Overview

This is a simple Django project that currently includes:

- A root "Hello World" page.
- Integration with `django-allauth` for user signup/login functionality.

### Features

- **Hello World Page:** Accessible at the root of the application.
- **User Authentication:** Provided by `django-allauth`, which supports user registration, login, and social account integration.

## Prerequisites

- Python 3.9.6
- PostgreSQL
- pip (Python package installer)
- Virtualenv (virtual environment manager for Python)

## Installation

### Clone the Repository

```sh
git clone https://github.com/yourusername/djangoProject.git
cd djangoProject
```

### Set Up Virtual Environment

```sh
python3 -m venv venv
source venv/bin/activate
```

### Install Dependencies

```sh
pip install -r requirements.txt
```

### Configure Environment Variables

Create a `.env` file in the root directory of your project and add the following environment variables:

```ini
# .env file
DB_NAME=your_db_name
DB_USER=your_db_user
DB_PASSWORD=your_db_password
DB_HOST=your_db_host
DB_PORT=your_db_port
SECRET_KEY=your_secret_key
DEBUG=True
ALLOWED_HOSTS=localhost,127.0.0.1
```

### Database Setup

Ensure that your PostgreSQL service is running and create the necessary database and user.

1. **Create Database:**
   
   ```sh
   createdb your_db_name
   ```

2. **Create User and Set Password:**
   
   ```sh
   createuser your_db_user
   psql -c "ALTER USER your_db_user WITH PASSWORD 'your_db_password';"
   ```

3. **Grant Privileges:**
   
   ```sh
   psql -c "GRANT ALL PRIVILEGES ON DATABASE your_db_name TO your_db_user;"
   ```

### Run Migrations

Apply database migrations to set up the database schema.

```sh
python manage.py migrate
```

### Create Superuser

Create a superuser to access the Django admin interface.

```sh
python manage.py createsuperuser
```

### Run the Development Server

Start the Django development server.

```sh
python manage.py runserver
```

You can access the application at `http://localhost:8000`.

## Project Structure

- **hello_world:** Contains the logic for the "Hello World" page.
- **users:** Configuration for user authentication using `django-allauth`.

## Environment Variables

Make sure to configure the necessary environment variables in your `.env` file as shown above. These settings are required for the application to run properly.

### settings.py Configuration

Your `settings.py` file should be configured to read from the environment variables. Example:

```python
import os
from pathlib import Path
from dotenv import load_dotenv

load_dotenv()

DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': os.getenv('DB_NAME'),
        'USER': os.getenv('DB_USER'),
        'PASSWORD': os.getenv('DB_PASSWORD'),
        'HOST': os.getenv('DB_HOST'),
        'PORT': os.getenv('DB_PORT', '5432'),
    }
}

SECRET_KEY = os.getenv('SECRET_KEY')
DEBUG = os.getenv('DEBUG', 'False').lower() in ['true', '1', 'yes']
ALLOWED_HOSTS = os.getenv('ALLOWED_HOSTS', '').split(',')
```

## Contributing

If you would like to contribute to this project, please submit a pull request or open an issue on the GitHub repository.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for more details.