---
title: DictCursor
subtitle: Using Psycopg2 Cursors like a Python Dict
date: 2018-12-10
img: icons8-postgresql-480.png
category: [programming, python, postgres, psycopg]
---
Recently, I was looking for a way to make working with psycopg2 cursors in python even more convenient. I stumbled across the [psycopg2 DictCursor Documentation](http://initd.org/psycopg/docs/extras.html#dictionary-like-cursor). This feature is pretty handy since you can use cursor objects like python dicts. This means that you can address columns of your fetched row by simplay putting the column name in sqaured brackets:
```python
import psycopg2
import psycopg2.extras
connection = psycopg2.connect(
    "put-your-connection-string-here",
    connection_factory=psycopg2.extras.DictConnection
)
with connection.cursor() as cur:
    cur.execute("SELECT * FROM customer;")
    for customer in cur:
        print(customer["name"])
```