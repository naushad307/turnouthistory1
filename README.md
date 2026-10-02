# Replacement History — MongoDB Full Database

This version removes browser `localStorage` as the application database. Records, columns, section opening dates, yearly GMT settings and security credentials are stored server-side in MongoDB.

## 1. Install
```bash
npm install
```

## 2. Configure
Copy `.env.example` to `.env` and set:
- `MONGODB_URI` — MongoDB Atlas connection string
- `JWT_SECRET` — long random server secret
- `PORT` — normally 3000

## 3. Run
```bash
npm start
```
Open `http://localhost:3000`.

## 4. First security-code setup
On first use, the app calls `/api/auth/setup` and stores a bcrypt hash in MongoDB. The recovery key is generated server-side and shown once. It is also stored only as a hash.

## API
- GET `/api/state` — read application data
- POST `/api/auth/setup` — first-time security setup
- POST `/api/auth/unlock` — verify security code and receive edit token
- PUT `/api/state` — save the complete application state
- POST `/api/auth/change` — change code
- POST `/api/auth/reset` — reset code with recovery key

## Important
Do not put the MongoDB username/password in frontend HTML or JavaScript. Only the Node.js server should know `MONGODB_URI`.
