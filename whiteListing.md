# Escaping is not always enough

## 🧩 What parameterized queries do

Parameterized queries (also called prepared statements) protect against SQL injection by treating user-supplied values as data, never as SQL code.

Example:

```
db.query("SELECT * FROM users WHERE email = ?", [userInput]);
```

Here, userInput is safely inserted as a value, not executable SQL.

If the user types:
```
' OR 1=1; --
```

## ⚠️ What they can’t do

Prepared statements only parameterize data values, not SQL identifiers or keywords.
That means you can’t safely substitute:
	•	Table names
	•	Column names
	•	ORDER BY columns
	•	Operators
	•	SQL keywords (ASC, DESC, LIMIT, etc.)

Example of something not safe or supported:

js 
```
// ❌ This cannot be parameterized
db.query("SELECT ?? FROM users ORDER BY ??", [columnName, sortOrder]);
```

Most database drivers won’t even let you bind these as parameters — and if you concatenate them yourself:

```
db.query(`SELECT ${columnName} FROM users ORDER BY ${sortOrder}`);
```

…you’ve opened the door to injection:

```
columnName = "email; DROP TABLE users; --"
```

## 🧠 Why escaping isn’t enough

You might think, “OK, I’ll just escape the string.”
But escaping is context-sensitive: different databases have slightly different identifier quoting rules ("column", [column], `column`), and user input could still break out of them if you miss a case or allow reserved words.
That’s why ASVS says:

“Query parts such as table and column names cannot be escaped.”

They mean: there’s no universal, guaranteed-safe way to escape arbitrary user input into those positions.

⸻

✅ Safe design patterns
	1.	Whitelisting

js
```
const allowedColumns = ['name', 'email', 'created_at'];
if (!allowedColumns.includes(req.query.sort)) {
  throw new Error('Invalid column');
}
const column = req.query.sort;
db.query(`SELECT name, email FROM users ORDER BY ${column}`);
```
Only approved identifiers ever appear in the SQL.

	2.	Fixed query shapes
Instead of building dynamic SQL strings, design separate queries:

js
```
if (sort === 'date') {
  db.query("SELECT * FROM users ORDER BY created_at DESC");
} else if (sort === 'name') {
  db.query("SELECT * FROM users ORDER BY name ASC");
}
```

3.	ORMs or query builders
Tools like Sequelize, Knex, Prisma, etc., enforce internal escaping and structure your query safely when possible — but you still need to whitelist when dealing with dynamic identifiers.

## 💡 Summary
- Parameterized queries protect values (e.g., WHERE email = ?) ✅
	
- They do not protect SQL identifiers (e.g., column, table names) 🚫
	
- Escaping alone isn’t safe for those fields.

- Use whitelisting or predefined query paths for anything dynamic.