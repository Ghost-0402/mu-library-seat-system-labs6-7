# MU Library Seat Management System: Labs 6 and 7 (Group O, ICT461)

- `before/`  Lab 5 app, kept as the vulnerable BEFORE version (run_before.py, port 5001)
- `app/`     hardened AFTER app (Lab 6): ownership tokens, CSP nonce, SSRF guard, env validation, 19 tests
- `lab7/`    PostgreSQL tier: Alembic migrations, repo with ACID transactions, pool, seed, benchmarks, stress scripts
- `evidence/` logs, screenshots and scripts behind every claim in the report

## Run the Lab 6 app
cd app; pip install -r requirements.txt; copy .env.example to .env and fill in values
(MU_SECRET_KEY 32+ chars, MU_ADMIN_PIN 8+ chars). `python app.py` refuses to start if they are missing.
Tests: `python -m unittest tests.test_security -v`

## Run Lab 7
1. Install PostgreSQL 16 and create a database and user; copy lab7/.env.example to .env and set DATABASE_URL and pool values.
2. `pip install "psycopg[binary]" psycopg_pool alembic sqlalchemy waitress flask`
3. `cd lab7; alembic upgrade 0001; python seed.py; python explain_bench.py` (baseline), `alembic upgrade head`, then rerun explain_bench.py
4. `python tx_demo.py` (transactions), `python leak_demo.py`, then `bash stress.sh` (needs Node and `npm i autocannon`).
Real .env files, keys and databases are intentionally not included.
