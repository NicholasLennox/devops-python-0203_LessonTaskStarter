# Bookshelf API

A small Flask API for managing a catalogue of books. It ships with a Dockerfile, a Gunicorn startup command and a pytest test suite.

## Setup

Create and activate a virtual environment:

```bash
python -m venv venv
```

Activate:

```bash
# Mac and Linux
source venv/bin/activate

# Windows - Git Bash
source venv/Scripts/activate

# Windows - Command Prompt
venv\Scripts\activate

# Windows - PowerShell
venv\Scripts\Activate.ps1
```

Install dependencies:

```bash
pip install -r requirements.txt
```

Copy `.env.example` to `.env` and fill in the values:

```bash
cp .env.example .env
```

## Running the Tests

```bash
python -m pytest
```

## Running the API

Mac and Linux:

```bash
gunicorn --bind 0.0.0.0:8000 src.app:app
```

Windows:

```bash
FLASK_APP=src/app.py flask run
```

## Docker

Build the image:

```bash
docker build -t books-api .
```

Run the container:

```bash
docker run -d -p 9000:8000 --env-file .env books-api
```

Run the tests inside the container:

```bash
docker run --env-file .env books-api python -m pytest
```

## Endpoints

| Method | Path | Description |
|--------|------|-------------|
| GET | /health | Health check - returns environment info |
| GET | /books | Get all books (optional `?author=` filter) |
| GET | /books/{id} | Get a book by ID |
| POST | /books | Create a new book (`title` and `author` required) |
| PUT | /books/{id} | Update a book (`title` and `author` required) |
| DELETE | /books/{id} | Delete a book |

## Configuration

| Variable | Description | Default |
|----------|-------------|---------|
| ENVIRONMENT | Environment name | none - required by the test suite |

See `.env.example` for the expected format.
