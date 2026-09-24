# Lost & Found Website — Vercel Ready

This is the Flask lost-and-found website, prepared for deployment on Vercel.

## Important: database

Vercel runs Flask as serverless compute, so the local `lost_found.db` file should **not** be used as the production database. This version uses:

- SQLite automatically when running locally without `DATABASE_URL`.
- PostgreSQL automatically when `DATABASE_URL` is set (recommended for Vercel).

Vercel currently supports Flask directly, so no `/api` rewrite is required.

## Deploy to Vercel

### 1. Create a Postgres database

In your Vercel project, add a Postgres database integration such as **Neon** from the Vercel Marketplace. It will provide a PostgreSQL connection string such as `DATABASE_URL`.

### 2. Add environment variables

In Vercel Project Settings → Environment Variables, add:

```text
DATABASE_URL=your-postgresql-connection-string
SECRET_KEY=a-long-random-secret
```

Use the same variables for Production (and Preview if you want preview deployments to use the database).

### 3. Deploy this folder

You can import this project into Vercel from GitHub, or run:

```bash
npm i -g vercel
vercel login
vercel
```

For production:

```bash
vercel --prod
```

### 4. Existing data

The included `lost_found.db` is kept for local development and as the source for an optional migration.

If you want to move the existing users/items into your new PostgreSQL database, install the requirements and run:

```bash
pip install -r requirements.txt
```

Set `DATABASE_URL`, then:

```bash
python migrate_sqlite_to_postgres.py
```

After migration, the same usernames/passwords and listings will be in PostgreSQL.

## Run locally

```bash
pip install -r requirements.txt
python app.py
```

Open `http://127.0.0.1:5000`.

Without `DATABASE_URL`, the app uses the included `lost_found.db`.

## Pages

- Login / Register
- Home dashboard
- Report lost item
- Report found item
- Search listings
- Item details
- User profile

## Project structure

```text
lost_found_website/
├── app.py
├── requirements.txt
├── vercel.json
├── .env.example
├── .gitignore
├── migrate_sqlite_to_postgres.py
├── lost_found.db
├── static/
│   └── style.css
└── templates/
    ├── base.html
    ├── login.html
    ├── register.html
    ├── home.html
    ├── items.html
    ├── item_detail.html
    ├── item_form.html
    └── profile.html
```
