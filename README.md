# StudyBuddy

StudyBuddy is a real-time discussion platform where users can create topic-based study rooms, chat with other participants, and follow activity across the community. Think of it as a lightweight Discord-meets-Reddit, built entirely with Django.

## What it does

- Users sign up with an email and set up a profile with a bio and avatar
- Anyone can create a "room" tied to a topic (e.g., Python, Machine Learning, DSA)
- Other users join rooms and participate in live conversations
- A global activity feed shows recent messages across all rooms
- Room hosts can edit or delete their rooms; message authors can delete their own messages
- A REST API exposes room data for external consumption

## Tech Stack

- **Backend:** Django 5.1, Django REST Framework
- **Database:** SQLite (default, easy to swap for PostgreSQL)
- **Auth:** Custom user model with email-based login
- **Frontend:** Django templates, vanilla CSS, minimal JavaScript
- **API:** DRF with CORS support via `django-cors-headers`

## Project Structure

```
studybuddy/
├── base/                        # Core Django app
│   ├── api/                     # REST API (DRF)
│   │   ├── serializers.py
│   │   ├── urls.py
│   │   └── views.py
│   ├── migrations/
│   ├── templates/base/          # App-level templates
│   │   ├── home.html
│   │   ├── room.html
│   │   ├── profile.html
│   │   ├── login_register.html
│   │   ├── room_form.html
│   │   ├── topics.html
│   │   ├── activity.html
│   │   ├── update-user.html
│   │   ├── delete.html
│   │   └── *_component.html     # Reusable partials
│   ├── admin.py
│   ├── apps.py
│   ├── forms.py
│   ├── models.py
│   ├── urls.py
│   └── views.py
├── studybuddy_config/           # Django project config
│   ├── settings.py
│   ├── urls.py
│   ├── asgi.py
│   └── wsgi.py
├── templates/                   # Global templates (base layout, navbar)
│   ├── main.html
│   └── navbar.html
├── static/
│   ├── images/                  # Icons, logo, default avatar
│   ├── js/
│   │   └── script.js
│   └── styles/
│       └── style.css
├── manage.py
├── requirements.txt
└── .gitignore
```

## Getting Started

**1. Clone the repo**

```bash
git clone https://github.com/your-username/studybuddy.git
cd studybuddy
```

**2. Create a virtual environment and install dependencies**

```bash
python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate
pip install -r requirements.txt
```

**3. Set up the database**

```bash
python manage.py migrate
```

This creates a local `db.sqlite3` file in the project root — no database server or credentials needed. SQLite is file-based and Django handles everything automatically. If you want to start with some sample data, you can create a superuser with `python manage.py createsuperuser` and use the admin panel at `/admin/`.

**4. Run the development server**

```bash
python manage.py runserver
```

Visit `http://127.0.0.1:8000` — that's it.

## API Endpoints

The project exposes a simple read-only REST API:

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/` | List available routes |
| GET | `/api/rooms/` | All rooms |
| GET | `/api/rooms/:id/` | Single room details |

## Data Models

**User** — extends Django's `AbstractUser`. Login is email-based. Stores a bio and an avatar image.

**Topic** — a simple label like "Python" or "Algorithms". Rooms are grouped under topics.

**Room** — the main entity. Has a host, a topic, a name, a description, and tracks participants and timestamps.

**Message** — belongs to a user and a room. Ordered by most recent first.


## Contributing

Pull requests are welcome. For larger changes, open an issue first so we can discuss what you'd like to change.
