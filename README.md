# Brainware University Canteen

Full-stack canteen ordering app — React + Vite frontend and Express + MongoDB backend.

## Key features
- User signup / login (hashed passwords with bcrypt)
- Add/update cart stored on user document
- Simple order history + user profile
- React frontend with routing (Vite + Tailwind)

## Tech stack
- Frontend: React, Vite, TailwindCSS
- Backend: Node.js, Express, Mongoose (MongoDB)
- Auth: bcrypt for password hashing

## Quick start

1. Clone the repo

2. Install dependencies

```bash
# install server deps
cd server
npm install

# install frontend deps
cd ../canteen
npm install
```

3. Configure environment for server

Create a `.env` file inside the `server/` folder with at least:

```
MONGO_URI=<your_mongodb_connection_string>
PORT=2007
```

4. Run the app

```bash
# start backend (from server/)
npm run start

# start frontend (from canteen/)
npm run dev
```

Open the frontend URL shown by Vite (usually http://localhost:5173) and ensure the backend is running at the `PORT` you set.

## Available scripts

- Frontend (in `canteen/`):
  - `npm run dev` — start Vite dev server
  - `npm run build` — build production bundle
  - `npm run preview` — preview production build

- Server (in `server/`):
  - `npm run start` — start server with `nodemon` (auto-restart)

The repository root also contains a `package.json` with dev dependencies used in the project.

## Backend API (important endpoints)

- `POST /signup` — create user
  - body: `{ studentCode, password, name, email, phoneNumber, ... }`

- `POST /login` — authenticate
  - body: `{ studentCode, password }`

- `POST /add-to-cart` — push an item into user's cart
  - body: `{ studentCode, item }` where `item` contains `name`, `price`, `image`, `quantity`, etc.

- `POST /update-cart` — replace the user's cart array
  - body: `{ studentCode, cart }` where `cart` is an array of cart item objects

- `GET /user?studentCode=...` — fetch user document by `studentCode`

Server implementation: [server/index.js](server/index.js)

## Project structure

- [server/](server/) — Express API and Mongoose models
  - [server/index.js](server/index.js) — server entry and routes
  - [server/Models/UserModel.js](server/Models/UserModel.js) — user schema with `cart` and `orders`
  - [server/Models/Product.js](server/Models/Product.js) — product schema

- [canteen/](canteen/) — React frontend (Vite)
  - [canteen/src/App.jsx](canteen/src/App.jsx) — routes and main layout
  - [canteen/src/main.jsx](canteen/src/main.jsx) — entry point
  - [canteen/src/Components/](canteen/src/Components/) — UI components

## Notes and recommendations
- Secure your `.env` and do not commit secrets.
- Consider adding proper authentication (JWT/session) for production instead of only returning user objects on login.
- Validate and sanitize inputs on the backend before saving to the database.

If you want, I can also:
- add example `.env.example`
- add npm workspace configuration to manage both client and server from root
- improve the README with screenshots and API examples (cURL / Postman)