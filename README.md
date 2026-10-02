# Wishme – birthday cake booking (real website)

Customers book without login. Owner (admin) and delivery partners log in with "Staff login".
Node.js + Express + SQLite. Files: server.js, index.html, package.json.

## Environment variables (set these on Render)
- ADMIN_PHONE  – owner's 10-digit mobile (this is the owner login)
- ADMIN_PASS   – owner's password (change it here any time, then redeploy)
- JWT_SECRET   – any long random text
- DB_PATH      – optional, e.g. /data/wishme.db when a persistent disk is attached

## Render settings
Build command: npm install   |   Start command: npm start

## Changing things later
Edit index.html (design, cakes, prices on screen) or server.js (rules, prices) on GitHub.
Render redeploys automatically in a few minutes. Cake prices must match in BOTH files.
