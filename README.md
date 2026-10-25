# CivicFix Smart Infrastructure Monitoring

## Project contents
- `app.py`: Flask web application and ESP32 telemetry API
- `templates/`: HTML pages used by Flask
- `static/`: CSS and uploads folder
- `requirements.txt`, `runtime.txt`, `Procfile`, `render.yaml`: Render deployment configuration
- `firmware/`: ESP32 Arduino sketch (not required for the Render web deployment)

## Deploy to Render
1. Upload the contents of this project to a GitHub repository. Keep `.gitignore` in the repository.
2. In Render, create a new **Blueprint** from that repository, or create a Python web service using `render.yaml`.
3. Confirm the service environment variables include `SECRET_KEY` and `ESP32_DEVICE_TOKEN`. The supplied `render.yaml` asks Render to generate values for these.
4. After deployment, open `/healthz` on your deployed site. It should return a healthy response.
5. Configure the ESP32 sketch with your actual Wi-Fi credentials, deployed API URL, the same `ESP32_DEVICE_TOKEN` value from Render, and the correct site address/coordinates. Then compile and upload the sketch.

## Important
- Do **not** upload `complaints.db`, `.env`, passwords, or real device tokens to GitHub.
- The database is intentionally not included in this ZIP. The app can initialize its SQLite database, but SQLite data on a typical Render web service filesystem may not persist across redeploys/restarts. Use a persistent disk or PostgreSQL for durable production data.
- Do not share the ESP32 device token publicly.
- The ESP32 firmware is included for convenience, but it is not part of the Render web build.
