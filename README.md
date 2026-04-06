# Symfony Course — Project Setup

This repository contains the code for the Symfony course. This README explains how contributors or students can start the project locally.

## Requirements

- PHP 8.1+ (check `composer.json` for exact requirement)
- Composer (https://getcomposer.org)
- A web server or the Symfony CLI (optional but recommended)
- Node.js (16+) and npm or pnpm if you want to build frontend assets
- A database supported by Doctrine (SQLite, MySQL, PostgreSQL)

## Quick start (development)

1. Clone the repository

```bash
git clone <repo-url> symfony-course
cd symfony-course
```

2. Install PHP dependencies

```bash
composer install
```

3. Copy environment variables

```bash
cp .env .env.local
# Edit .env.local and set DATABASE_URL and other secrets as needed
```

4. Create the database and run migrations

If you use SQLite (default in many dev setups):

```bash
# ensure directory for sqlite file exists if used
php bin/console doctrine:database:create
php bin/console doctrine:migrations:migrate
```

For MySQL/Postgres, set `DATABASE_URL` in `.env.local` to the correct DSN and then run the same migrate command.

5. Load fixtures (if present)

```bash
php bin/console doctrine:fixtures:load
```

This may prompt to purge the database first — read the prompt carefully.

6. Install frontend dependencies and build assets (optional)

If you plan to work on frontend assets in the `assets/` directory:

```bash
npm install
# or: pnpm install
npm run dev
# or production build: npm run build
```

7. Run the app locally

Recommended: use the Symfony CLI (https://symfony.com/download)

```bash
symfony server:start
# or if you don't have symfony CLI, use PHP built-in server
php -S 127.0.0.1:8000 -t public
```

Open http://127.0.0.1:8000 in your browser.

## Running tests

This project includes tests. Run them with PHPUnit:

```bash
# Use the phpunit binary shipped with the repo
./bin/phpunit
```

If you get missing extensions or failures, ensure `composer install` completed and the test database is configured.

## Useful console commands

- List available commands:

```bash
php bin/console list
```

- Clear cache (environment `dev` or `prod`):

```bash
php bin/console cache:clear
```

- Create a new migration after changing entities:

```bash
php bin/console make:migration
php bin/console doctrine:migrations:migrate
```

## Environment variables

- Use `.env` as reference. Copy to `.env.local` and do NOT commit `.env.local`.
- Common variables: `APP_ENV`, `APP_SECRET`, `DATABASE_URL`, `MAILER_DSN`.

## Troubleshooting

- Composer memory issues: `COMPOSER_MEMORY_LIMIT=-1 composer install`
- Permissions on `var/` and `public/` (ensure your web server user can write to `var/` cache and log directories).
- If assets don't load, check `public/build` and run `npm run dev`.

## Contributing

If you want to improve course materials or add exercises, please:

1. Fork the repo
2. Create a feature branch
3. Open a PR with a clear description and steps to validate

## Notes for instructors

- The `tests/` folder contains example tests you can use to verify students' code.
- Consider providing a `.env.local` template or Docker/Compose setup if students use different platforms.

---

If you'd like, I can also:
- Add example `.env.local.dist` with recommended variables.
- Add a `Makefile` or `phpstorm-helpers` to make setup easier.

Let me know which extras you prefer.
