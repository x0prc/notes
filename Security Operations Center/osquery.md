---
{"dg-publish":true,"permalink":"/src/site/notes/src/site/notes/src/site/notes/src/site/notes/main/cs/security-operations-center/osquery/"}
---






```JavaScript
osqueryi
```

- List the tables

```JavaScript
.table
```

- To list all the tables with the term `user` in them

```JavaScript
.table user
```

- Table schema

```JavaScript
.schema users
```

- SQL Query Syntax

```JavaScript
select gid, uid, description, username, directory from users;
```

## Exploring Installed Programs

```JavaScript
select * from programs limit 1;
	
select name, version, install_location, install_date from programs limit 1;
```

## Count

```JavaScript
select count(*) from programs;
```

## WHERE Clause

```JavaScript
SELECT * FROM users WHERE username='James';
```

## JOIN Function

```JavaScript
select p.pid, p.name, p.path, u.username from processes p JOIN users u on u.uid=p.uid LIMIT 10;
```