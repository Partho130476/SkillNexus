# Skill Nexus

A multi-role skill development and job marketplace platform built with **Django REST Framework**. Skill Nexus connects Students, Freelancers, Educators, Employers, and Universities on a single platform — enabling course enrollment, freelance job posting, university program applications, and more.

---

## Features

| Module | Description |
|---|---|
| **Auth** | JWT-based signup, login, role-based access |
| **User Profiles** | Personal details, education, training, experience |
| **Skills** | Skill catalog, per-user skill tracking |
| **Courses** | Educators create courses with lectures, videos, materials |
| **Enrollment** | Students enroll in courses, watch videos |
| **Freelancing** | Employers post jobs, freelancers apply and negotiate |
| **Messaging** | Job-linked messaging between employers and freelancers |
| **University** | Universities post programs/sessions, students apply |
| **Admin Panel** | User management, status control (Active/Banned/Suspended) |
| **Swagger UI** | Auto-generated API docs via drf-yasg |

### User Roles
`Student` · `Freelancer` · `Educator` · `Employer` · `University` · `Admin`

---

## Tech Stack

- **Backend:** Python 3, Django 4.2, Django REST Framework
- **Auth:** JWT (`djangorestframework-simplejwt`)
- **API Docs:** `drf-yasg` (Swagger / ReDoc)
- **Database:** SQLite (dev) · MySQL (production-ready)
- **Media:** Pillow (image uploads), file uploads for videos & syllabi
- **CORS:** `django-cors-headers`

---

## Project Structure

```
skill-nexus-main/
└── skillNexus/
    ├── backend/          # Django project settings, urls, wsgi/asgi
    ├── api/              # API views, URL routing, middleware
    ├── data/             # Models, serializers, admin, templates
    │   ├── models.py     # All DB models
    │   ├── serializers.py
    │   └── templates/    # PHP/HTML templates (legacy frontend)
    ├── test_data/        # Seed JSON fixtures
    ├── manage.py
    └── requirements.txt
```

---

## Getting Started

### Prerequisites
- Python 3.10+
- pip

### Installation

```bash
# 1. Clone the repo
git clone https://github.com/Partho130476/skill-nexus.git
cd skill-nexus/skillNexus

# 2. Create and activate a virtual environment
python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate

# 3. Install dependencies
pip install -r requirements.txt

# 4. Apply migrations
python manage.py migrate

# 5. Create a superuser (optional)
python manage.py createsuperuser

# 6. Run the development server
python manage.py runserver
```

The API will be available at `http://127.0.0.1:8000/`

---

## Environment Variables

Create a `.env` file in `skillNexus/` (or set these in your environment):

```env
SECRET_KEY=your-secret-key-here
DEBUG=True
DATABASE_URL=sqlite:///db.sqlite3   # or mysql://user:pass@host/dbname
```

> **Note:** Never commit your `.env` or `SECRET_KEY` to version control.

---

## Database (MySQL for production)

In `backend/settings.py`, uncomment and configure the MySQL block:

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'skillnexus',
        'USER': 'your_db_user',
        'PASSWORD': 'your_db_password',
        'HOST': 'localhost',
        'PORT': '3306',
    }
}
```

---

## API Documentation

Once running, visit:

- **Swagger UI:** `http://127.0.0.1:8000/swagger/`
- **ReDoc:** `http://127.0.0.1:8000/redoc/`

### Key Endpoints

| Method | Endpoint | Description |
|---|---|---|
| POST | `/api/signup` | Register a new user |
| POST | `/api/login` | Login, returns JWT tokens |
| GET | `/api/current_user` | Get authenticated user info |
| GET/POST | `/api/skills/all` | List all skills |
| POST | `/api/course/add` | Educator: create course |
| GET | `/api/course_list/get` | Browse all courses |
| POST | `/api/course_enroll/add` | Student: enroll in course |
| POST | `/api/university/program/add` | University: add program |
| POST | `/api/student/university/apply` | Student: apply to program |
| GET | `/api/admin/users` | Admin: list all users |

All protected endpoints require the header:
```
Authorization: Bearer <access_token>
```

---

## Seed Data

Test fixtures are available in `skillNexus/test_data/`:

```bash
python manage.py loaddata test_data/skill.json
python manage.py loaddata test_data/user.json
python manage.py loaddata test_data/company.json
python manage.py loaddata test_data/job.json
```

---

## Deployment (cPanel / Passenger)

A `passenger_wsgi.py` is included for shared hosting deployments via Passenger WSGI.

---

## Contributing

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/your-feature`
3. Commit your changes: `git commit -m "feat: add your feature"`
4. Push to your branch: `git push origin feature/your-feature`
5. Open a Pull Request

---

## License

This project is open source. Add your preferred license here.
