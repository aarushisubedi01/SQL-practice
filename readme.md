...existing code...
# SQL Learning Codespace — Detailed README

This codespace is an educational workspace demonstrating how to use the IPython SQL magic to create, populate, and query a local SQLite database from a Jupyter notebook. It is intended for learning schema design, inserts, joins, aggregations, and basic troubleshooting.

Files in this workspace
- [learning_sql.ipynb](learning_sql.ipynb) — primary notebook containing all SQL cells, table schemas, inserts, and queries.
- [requirements.txt](requirements.txt) — Python packages required to run the notebook.
- [readme.md](readme.md) — this file.

Key commands and notebook flow
- Load SQL magic: use the cell `%load_ext sql` (see [`%load_ext sql`](learning_sql.ipynb) in the notebook).
- Connect to SQLite: use the cell `%sql sqlite:///newdb.db` (see [`%sql sqlite:///newdb.db`](learning_sql.ipynb)). This opens or creates `newdb.db` in the workspace root.
- Use cell magic `%%sql` for multi-line SQL statements. Examples in the notebook: [`%%sql`](learning_sql.ipynb).

Notebook structure (cell groups)
1. Environment & connection
   - `%load_ext sql` — enables `%%sql`.
   - `%sql sqlite:///newdb.db` — establishes the DB connection.

2. Schema creation
   - `CREATE TABLE employees (...)` — sample table for quick experimentation.
   - `CREATE TABLE customers (...)`, `hotels`, `rooms`, `bookings`, `payments` — relational schema demonstrating PKs, FKs and common column types. See the schema cells in [learning_sql.ipynb](learning_sql.ipynb).

3. Data population
   - Batched `INSERT INTO` statements populate each table with example rows. These insert cells are located in the notebook and use `%%sql` to run multi-row inserts.

4. Queries and examples
   - Basic selects: `SELECT * FROM customers;`
   - Filters: `WHERE city = 'Pokhara'`
   - Aggregation: `SELECT COUNT(*) FROM customers;`, `GROUP BY hotel_id`
   - Joins: example showing bookings for a customer with multiple JOINs between `bookings`, `customers`, `rooms`, and `hotels`.
   - Date range: `SELECT * FROM bookings WHERE check_in >= '2024-05-10' AND check_out <= '2024-05-31';` (see the related cell in [learning_sql.ipynb](learning_sql.ipynb)).

How to run locally in this codespace
1. Install dependencies listed in [requirements.txt](requirements.txt):
   ```
   python -m pip install -r requirements.txt
   ```
   Minimal required: `ipython-sql` and `sqlalchemy`. SQLite driver is in the Python stdlib.

2. Open [learning_sql.ipynb](learning_sql.ipynb) in VS Code or Jupyter and run cells top-to-bottom:
   - Run the `%load_ext sql` cell first.
   - Run the connection `%sql sqlite:///newdb.db`.
   - Run schema creation and insert cells, then run queries.

Implementation notes & best practices
- Primary keys: the notebook uses explicit integer PKs. For SQLite, consider `INTEGER PRIMARY KEY AUTOINCREMENT` for automatic id assignment.
- Foreign keys: SQLite requires PRAGMA foreign_keys = ON if you want enforcement; the notebook defines FK relationships for design clarity but SQLite may not enforce them by default.
- Transaction safety: for larger changes, wrap inserts in transactions or use parameterized inserts when using programmatic APIs.
- Persistent DB: `newdb.db` is created in the workspace root when the notebook runs. The notebook intentionally uses in-file SQLite for portability.

Troubleshooting
- "table ... already exists": rerun cells will fail if the table already exists. Use `DROP TABLE IF EXISTS table_name;` before `CREATE TABLE` or restart with a fresh `newdb.db`.
- UNIQUE/Integrity errors on inserts: ensure IDs are unique or switch to AUTOINCREMENT for id columns.
- If a `%%sql` cell shows syntax/format errors, ensure the cell begins exactly with `%%sql` on its own line (see examples in [learning_sql.ipynb](learning_sql.ipynb)).

Extending the workspace
- Add more normalized tables (e.g., `departments`, `amenities`) and sample data.
- Move from raw SQL cells to programmatic access using SQLAlchemy or pandas for richer analysis.
- Add tests or small scripts to validate referential integrity and expected aggregates.

References inside the workspace
- Notebook: [learning_sql.ipynb](learning_sql.ipynb)
- Requirements: [requirements.txt](requirements.txt)
- Sample SQL commands referenced: [`%load_ext sql`](learning_sql.ipynb), [`%sql sqlite:///newdb.db`](learning_sql.ipynb), [`%%sql`](learning_sql.ipynb)

