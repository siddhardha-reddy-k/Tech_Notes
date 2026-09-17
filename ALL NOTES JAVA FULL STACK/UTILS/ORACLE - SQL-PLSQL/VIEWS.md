- Simple View
- Complex View
- WITH READ ONLY
- WITH CHECK OPTION
- Materialized View

## VIEW — What it actually is

A view is a **stored query**, not stored data. When you create one, Oracle saves the SELECT statement itself under a name. Every time you query the view, Oracle re-runs that saved SELECT against the live base table.

```sql
CREATE VIEW v1
AS
SELECT * FROM emp;
```

```sql
SELECT * FROM v1;
```

**What actually happens when you run that second query:** Oracle doesn't have a separate copy of emp's data sitting inside v1. It looks up v1's definition, sees it's SELECT * FROM emp, and runs that against the *current* emp table right then. So if you insert a new employee into emp, and query v1 a second later, the new employee shows up in v1 too — automatically, no refresh needed.

**Why this matters — the core mental shift from tables:**

- A table = physical data on disk.
- A view = **no data of its own** — just a saved query that runs live every time.

**Why use a view at all, then, if it's just a saved query?**

1. **Simplifies repeated complex queries — instead of retyping a 3-table join every time, save it once as a view.**
2. **Restricts access — give someone a view showing only certain columns/rows, hide the rest of the real table.**
3. **Abstraction layer — if the underlying table structure changes, you can often just update the view definition, and anyone using the view doesn't need to change their queries.**

## SIMPLE VIEW

A view built from **one base table**, with no joins, no grouping, no aggregate functions.

```sql
CREATE VIEW v1
AS
SELECT eid, ename, esal
FROM emp;

SELECT * FROM v1;
```

We can run DataManipulationLanguage commands(DML) with simple view as there is only one table.

```sql
UPDATE v1 SET esal = 47000 WHERE eid = 101;
```

This actually updates Alan's esal in the real emp table — the view is just a lens, but writes pass through to the base table underneath.

```sql
INSERT INTO v1 VALUES (107, 'Sunil', 42000);
```

This works too — but notice v1 only exposes eid, ename, esal, not deptno. So this insert creates a real row in emp with **deptno = NULL** (since it wasn't provided and has no default) — Oracle fills unlisted columns with NULL if they're nullable, or errors out if that column is NOT NULL and has no default.

## COMPLEX VIEW

Built from **multiple tables** (joins), or includes grouping, aggregates, expressions — anything beyond a straight one-table SELECT.

```sql
CREATE VIEW v2
AS
SELECT e.eid, e.ename, e.esal, d.dname, d.dloc
FROM emp e
JOIN dept d
ON e.deptno = d.deptno;

SELECT * FROM v2;
```

```text
EID  ENAME   ESAL    DNAME     DLOC
101  Alan    45000   HR        Hyderabad
102  Raja    52000   IT        Bangalore
103  Priya   41000   HR        Hyderabad
104  Kiran   60000   IT        Bangalore
105  Meena   38000   Finance   Chennai
```

Same 5 rows as our earlier INNER JOIN — David and Sales excluded, exactly like before. The view just wraps that join query under a name.

Updating dname through v2 fails because dname belongs to dept, and one dept row (deptno 10) is shared by multiple employees (Alan + Priya). Oracle can't tell which employee's department you actually meant to change, so it blocks it to avoid silently affecting other rows.

**General rule:** DML on a complex view fails when it's ambiguous — i.e., one view row maps back to multiple base-table rows, or the view uses grouping/aggregates.

**What might still work:** updating a column that belongs to only one table and isn't part of the join (e.g., esal, purely from emp) — but this gets unreliable fast, which is why WITH READ ONLY exists: to remove the guesswork entirely.

## WITH READ ONLY

Explicitly blocks **all** DML (INSERT/UPDATE/DELETE) through a view — no ambiguity, no case-by-case guessing like complex views had. A hard rule you set on purpose.

```sql
CREATE VIEW v3
AS
SELECT * FROM emp
WITH READ ONLY;
```

```sql
DELETE FROM v3 WHERE eid = 106;
```

**Result:** fails — Oracle throws an error like ORA-01732: data manipulation operation not legal on this view, regardless of whether the DML would've been "safe" or not.

## WITH CHECK OPTION

Ensures that DML through a view **cannot create or update a row that would violate the view's own WHERE condition** — i.e., you can't insert/update data through the view that the view itself wouldn't be able to show you afterward.

```sql
CREATE VIEW v4
AS
SELECT * FROM emp
WHERE deptno = 10
WITH CHECK OPTION;
```

v4 only shows employees in dept 10 (Alan, Priya).

```sql
INSERT INTO v4 VALUES (107, 'Sunil', 42000, 10);
```

Works — deptno = 10 matches the view's WHERE clause, so the new row is something v4 itself would display.

Invalid insert — violates the condition:

```sql
INSERT INTO v4 VALUES (108, 'Kavya', 39000, 20);
```

**Why this matters — the real problem it solves:** without WITH CHECK OPTION, that same insert (deptno = 20) would actually **succeed** silently. The row gets added to the real emp table just fine — but then if you immediately SELECT * FROM v4, Kavya **won't show up**, because she doesn't match deptno = 10. That's a confusing, invisible mismatch: you inserted through v4, but v4 can't show you what you just inserted.

## MATERIALIZED VIEW

Unlike a normal view (which stores only the query, re-running it live every time), a materialized view **physically stores the actual result data** — like a snapshot of the query, saved to disk.

```sql
CREATE MATERIALIZED VIEW v5
AS
SELECT * FROM emp;

SELECT * FROM v5;
```

**What's actually different, mechanically:**

- **Normal view (v1-v4):** querying it = Oracle re-executes the SELECT live against emp, every single time. Zero storage cost, always current.
- **Materialized view (v5):** querying it = Oracle just reads the **stored snapshot**. No re-execution of the underlying query happens at read time — it's genuinely faster for expensive queries (heavy joins, aggregates over millions of rows), because that heavy computation already happened once, at creation/refresh time.

Materialized view stores actual data, not just the query — so it doesn't auto-update when emp changes. You have to manually refresh it (DBMS_MVIEW.REFRESH) to see new data.

**Why it's worth it:** for heavy queries (big joins, millions of rows), recalculating live every time is slow. Materialized view pays that cost once, then serves fast reads from the saved snapshot — refresh on a schedule instead of every query. Common in reporting/dashboards where slightly old data is fine.

## VIEW LIST Listing all views you've created:

```sql
SELECT view_name
FROM user_views;
```

## DROP VIEW

```sql
DROP VIEW v1;
```

Dropping a materialized view — slightly different:

```sql
DROP MATERIALIZED VIEW v5;
```
