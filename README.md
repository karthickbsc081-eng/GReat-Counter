# Hotel Counter Manager

A full-stack web app for managing omelette and dosa counters in a hotel.
Built with Flask + SQLite backend, single-file frontend — no build step required.

---

## Quick Start (Local)

```bash
# 1. Install dependencies
pip install -r requirements.txt

# 2. Run the app
python app.py

# 3. Open in browser
# http://localhost:5000

# Default admin login
# Employee ID: ADMIN
# Password:    admin123
```

---

## Features

**Staff view**
- Select omelette or dosa counter
- Pick a variety (shown as icon cards)
- Enter alphanumeric table number (A5, VIP1, T12, etc.)
- Set quantity and optional notes
- View pending orders with live elapsed timer
- Mark orders complete — delivery time is recorded

**Admin view**
- Manage varieties: add/remove with custom icon for each counter
- Manage users: create staff/admin accounts with employee ID + password
- Reports: filter by date, counter, status — see delivery time per order

---

## Deployment Options

### Option 1: Railway (recommended, free tier available)

1. Push to a GitHub repo
2. Go to https://railway.app → New Project → Deploy from GitHub
3. Set these environment variables in Railway dashboard:
   - `SECRET_KEY` = any long random string
   - `PORT` = 5000 (Railway sets this automatically)
4. Done — Railway auto-detects Flask and deploys

### Option 2: Render (free tier)

1. Push to GitHub
2. Go to https://render.com → New → Web Service
3. Connect your repo
4. Build command: `pip install -r requirements.txt`
5. Start command: `python app.py`
6. Set env var `SECRET_KEY` to a random string
7. Deploy

### Option 3: PythonAnywhere (free tier)

1. Sign up at https://www.pythonanywhere.com
2. Upload `app.py` and `requirements.txt` via Files tab
3. Go to Web tab → Add a new web app → Flask
4. Set source code path to `/home/<username>/app.py`
5. In the WSGI file, change the import to point to your app
6. Install requirements in a Bash console: `pip install -r requirements.txt`
7. Reload the web app

### Option 4: VPS / Ubuntu Server

```bash
# Install
sudo apt update && sudo apt install python3-pip python3-venv -y
git clone <your-repo> counter-app
cd counter-app
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt gunicorn

# Run with gunicorn (production)
gunicorn -w 4 -b 0.0.0.0:5000 app:app

# Or set up as a systemd service for auto-restart
```

---

## Environment Variables

| Variable | Default | Description |
|----------|---------|-------------|
| `SECRET_KEY` | `hotel-counter-secret-2024-change-in-prod` | JWT signing key — **change this in production** |
| `DATABASE` | `counter.db` | SQLite database file path |
| `PORT` | `5000` | HTTP port |
| `DEBUG` | `false` | Enable debug mode |

---

## Data

- All data stored in `counter.db` (SQLite) — created automatically on first run
- To reset: delete `counter.db` and restart
- To back up: copy `counter.db`

---

## Tech Stack

- **Backend**: Python / Flask
- **Database**: SQLite (via Python stdlib — no extra install)
- **Auth**: JWT tokens (PyJWT)
- **Frontend**: Vanilla JS (no build step, no npm)
- **Icons**: Tabler Icons (CDN)
