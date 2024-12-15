# Library Management System API

A Django REST Framework-based Library Management System with book borrowing functionality and automated reporting features.

## Features

- Complete CRUD operations for Authors and Books
- Book borrowing and return system
- Automated report generation using Celery
- API Documentation with Swagger/OpenAPI
- Comprehensive test coverage
- User-friendly admin interface

## Tech Stack

- Python 3.9+
- Django 3.2
- Django REST Framework
- Celery
- Redis
- SQLite (default database)
- drf-yasg (API Documentation)

## Installation

1. Clone the repository
```bash
git clone https://github.com/NavalEP/Library-Management-System.git
```

2. Create and activate virtual environment
```bash
python3 -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

3. Install dependencies
```bash
pip3 install -r requirements.txt
```

4. Set up environment variables
Create a `.env` file in the root directory and add:
```
DEBUG=True
SECRET_KEY='django-insecure-savi)&k#su4*4(406b)o_9#7^b=hsz!18wtrs6il9=o_o6rw(9'
ALLOWED_HOSTS=localhost,127.0.0.1
CELERY_BROKER_URL=redis://localhost:6379/0
CELERY_RESULT_BACKEND=redis://localhost:6379/0
DATABASE_URL=sqlite:///db.sqlite3
```

5. Run migrations
```bash
python3 manage.py makemigrations
python3 manage.py migrate
```

6. Create superuser
```bash
python3 manage.py createsuperuser
```

## Running the Application

1. Start Redis server (required for Celery)
```bash
redis-server
```

2. Start Celery worker (open a new terminal)
```bash
celery -A library_project worker --loglevel=info
```

3. Run the development server (open a new terminal)
```bash
python3 manage.py runserver
```

## API Endpoints

### Authors
- `GET /api/authors/` - List all authors
- `POST /api/authors/` - Create a new author
- `GET /api/authors/{id}/` - Get author details
- `PUT /api/authors/{id}/` - Update author
- `DELETE /api/authors/{id}/` - Delete author

### Books
- `GET /api/books/` - List all books
- `POST /api/books/` - Add a new book
- `GET /api/books/{id}/` - Get book details
- `PUT /api/books/{id}/` - Update book
- `DELETE /api/books/{id}/` - Delete book

### Borrow Records
- `POST /api/borrow/` - Create new borrow record
- `PUT /api/borrow/{id}/return/` - Return a book

### Reports
- `GET /api/reports/` - Get latest report
- `POST /api/reports/` - Generate new report

## API Documentation
Access the interactive API documentation at:
- Swagger UI: `http://localhost:8000/swagger/`
- ReDoc: `http://localhost:8000/redoc/`

## Database Models

### Author
- name (CharField)
- bio (TextField, optional)
- created_at (DateTimeField)
- updated_at (DateTimeField)

### Book
- title (CharField)
- author (ForeignKey to Author)
- isbn (CharField, unique)
- available_copies (IntegerField)
- created_at (DateTimeField)
- updated_at (DateTimeField)

### BorrowRecord
- book (ForeignKey to Book)
- borrowed_by (CharField)
- borrow_date (DateField)
- return_date (DateField, nullable)
- created_at (DateTimeField)
- updated_at (DateTimeField)

## Report Generation
The system generates detailed reports including:
- Total number of authors
- Total number of books
- Currently borrowed books

Reports are generated asynchronously using Celery and stored in the `reports` directory.

## Running Tests
```bash
python3 manage.py test
```

## Admin Interface
Access the admin interface at `http://localhost:8000/admin/` using your superuser credentials.

## Error Handling
The API includes comprehensive error handling for:
- Invalid requests
- Resource not found
- Validation errors
- Database constraints
- Business logic violations

## Security Features
- Input validation
- CSRF protection
- SQL injection prevention
- Cross-Origin Resource Sharing (CORS) configuration
- Proper error messages without system information exposure

## Contributing
1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## License
This project is licensed under the MIT License - see the LICENSE file for details

