# GSQ-test-1
GSQ radio 
gsq-radio/
├── gsq_radio.py
├── requirements.txt
├── Dockerfile
├── README.md
└── static/
    └── index.html
# gsq_radio.py
# === Full Flask App Here ===
# Paste your full code here from earlier (you already have it).

# Example of the entry point:
if __name__ == "__main__":
    from pathlib import Path
    MEDIA_ROOT = Path.cwd() / "media"
    (MEDIA_ROOT / "music").mkdir(parents=True, exist_ok=True)
    (MEDIA_ROOT / "jingles").mkdir(parents=True, exist_ok=True)
    (MEDIA_ROOT / "ads").mkdir(parents=True, exist_ok=True)
    (Path.cwd() / "static").mkdir(parents=True, exist_ok=True)
    app.run(host="0.0.0.0", port=5000)
flask
flask_sqlalchemy
python-dateutil
FROM python:3.11-slim
WORKDIR /app
COPY . /app
RUN pip install -r requirements.txt
EXPOSE 5000
CMD ["python", "gsq_radio.py"]
# 🎵 GSQ Radio Scheduler

A Flask-based smart radio scheduler with support for:
- 🎶 Music and jingle rotation
- 📺 Advertising campaign control
- 🕒 Clock-based rotation rules
- 📈 Playback logging
- 🧠 Smart ad/hour constraints

## 📦 Requirements

```bash
pip install -r requirements.txt
python gsq_radio.py
docker build -t gsq-radio .
docker run -p 5000:5000 gsq-radio
http://localhost:5000/static/index.html

---

### 📁 `static/index.html`
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>GSQ Radio Dashboard</title>
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@picocss/pico@1/css/pico.min.css" />
</head>
<body>
<nav class="container-fluid">
  <ul><li><strong>GSQ Radio</strong></li></ul>
  <ul>
    <li><a href="/static/index.html">Dashboard</a></li>
    <li><a href="/api/nowplaying">Now Playing</a></li>
    <li><a href="/api/next">Next</a></li>
  </ul>
</nav>
<main class="container">
  <hgroup>
    <h2>GSQ Radio Admin</h2>
    <h3>Manage content, clocks, and campaigns</h3>
  </hgroup>

  <h3>Import Media</h3>
  <form method="POST" action="/admin/import/library">
    <button type="submit">Scan Library</button>
  </form>

  <h3>Seed Weekday/Weekend Clocks</h3>
  <form method="POST" action="/admin/clocks/seed_weekday_weekend">
    <button type="submit">Seed Clocks</button>
  </form>

  <h3>Now Playing</h3>
  <button onclick="fetchNowPlaying()">Refresh</button>
  <pre id="nowplaying"></pre>
</main>

<script>
function fetchNowPlaying() {
  fetch('/api/nowplaying')
    .then(res => res.json())
    .then(data => {
      document.getElementById('nowplaying').textContent = JSON.stringify(data, null, 2);
    });
}
</script>
</body>
</html>
git init
git add .
git commit -m "Initial commit for GSQ Radio Scheduler"
git remote add origin https://github.com/YOUR_USERNAME/gsq-radio.git
git push -u origin main
