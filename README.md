# SmartQrAtteandance

SmartQrAtteandance is a QR-based attendance application built with:
- Python + FastAPI backend
- SQLite database
- Android app in Kotlin
- QR scanning and attendance recording
- Attendance history and admin reporting
- JWT-based login for backend access

## Features
- Scan QR codes containing `user_id|event_id|timestamp`
- Mark attendance with timestamp and sync to SQLite
- View attendance history by user or event
- Login flow for app users
- Modern Android UI that looks production-ready
- GitHub Actions workflow to build an APK automatically

## Project structure
- `backend/` — FastAPI API and SQLite models
- `android/` — Android Kotlin project
- `.github/workflows/` — APK build workflow for GitHub Actions

## Backend setup

```bash
cd backend
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
uvicorn app.main:app --reload --host 0.0.0.0 --port 8000
```

### Default login user
The backend creates a default user when launched:
- Username: `admin`
- Password: `admin123`

### API endpoints
- `POST /auth/login` — login and receive token
- `POST /attendance/scan` — scan and record attendance
- `GET /attendance/history` — fetch attendance history
- `GET /attendance/report` — event summary report
- `POST /users` — create a user
- `POST /events` — create an event

## Android app setup

Open the `android/` folder in Android Studio and sync the project.

### Important config for the app
Change `BASE_URL` in `android/app/src/main/java/com/smartqratteandance/AttendanceApi.kt` to your backend URL:

```kotlin
private const val BASE_URL = "http://10.0.2.2:8000/"
```

For a physical device, replace it with your machine's LAN IP if needed.

## QR format
The app expects QR content in this format:

```text
user_id|event_id|timestamp
```

Example:

```text
U001|EVT-2026|2026-10-19T10:25:00Z
```

## APK build via GitHub Actions

A workflow lives in:
- `.github/workflows/android-build.yml`

When you push to `main` or trigger manually, it builds the Android debug APK and uploads it as an artifact. If a tag is pushed, it creates a release and uploads the APK as a release asset.

## Notes
- This is a production-style starter project with SQLite, JWT auth, QR attendance, and a clean Android UI.
- For a production deployment, replace SQLite with PostgreSQL and add stronger security controls.

## License
MIT
