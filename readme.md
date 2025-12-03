# SQL Learning Workspace

Overview
- This workspace demonstrates using the IPython SQL magic with a local SQLite database inside a Jupyter notebook (learning_sql.ipynb).
- Purpose: create a simple `employees` table, insert rows, and run queries while learning SQL via notebook cells.

Workspace files
- learning_sql.ipynb — main notebook. Cells:
  - Load SQL extension: `%load_ext sql`
  - Connect to SQLite DB: `%sql sqlite:///newdb.db`
  - Create table: `%%sql CREATE TABLE employees (...)`
  - Insert rows: `%%sql INSERT INTO employees VALUES (...)`
  - Query table: `%%sql SELECT * FROM employees;`
- newdb.db — SQLite database file (created at runtime when you first run the notebook).
- README.md — this file.

Notebook flow (cell-by-cell)
1. Load SQL extension
   - `%load_ext sql`
   - Enables `%%sql` cell magic.
2. Connect to database
   - `%sql sqlite:///newdb.db`
   - Creates or opens `newdb.db` in workspace root.
3. Create table
   - `%%sql` cell that runs `CREATE TABLE employees (id INT PRIMARY KEY, name VARCHAR(50), salary DECIMAL(10,2));`
   - Declares schema.
4. Insert rows
   - `%%sql INSERT INTO employees VALUES (1, 'Aarushi', 55000), (2, 'John', 60000);`
5. Select/query
   - `%%sql SELECT * FROM employees;`
   - Returns the inserted rows in notebook output.

How to run (Windows + VS Code)
1. Install dependencies:
   - Open integrated terminal and run:
     ```
     python -m pip install ipython-sql sqlalchemy
     ```
   - SQLite support is built into Python.
2. Open `learning_sql.ipynb` in VS Code or Jupyter.
3. Run cells in order. The `%sql` magic requires the extension load cell to run first.

Common issues & fixes
- If a `%%sql` cell shows a syntax error, ensure the cell starts with exactly `%%sql` on its own line (no stray quotes or punctuation).
- Example fix for a malformed SELECT cell (some cells in the file may contain stray characters like `%%sql",`):
  ```
  %%sql
  SELECT * FROM employees;
  ```
- If connection fails, confirm the connection line is: `%sql sqlite:///newdb.db`

Extending the notebook
- Add more tables (departments, projects).
- Use `AUTOINCREMENT` for id columns in SQLite if you want automatic ids.
- Explore joins, aggregations, and indexes.

Notes
- The notebook uses an in-file SQLite DB (`newdb.db`) so changes persist in the workspace folder.
- Keep cell order: extension → connection → schema → insert → queries.

License & Contribution
- This is an educational sample. Modify freely for learning.