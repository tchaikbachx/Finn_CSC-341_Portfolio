+++
date = '2026-04-08T08:19:13-05:00'
draft = false
title = 'Development'
+++
# Medium-scale Abstraction
For the functions which update entries, they need to only update the columns for which values are passed, without editing the columns that don't need to be updated. In order to do this, I initially used in-line conditionals to only include the columns for which values were non-null, but this ended up being quite unwieldy and needed to be tailor-made for each table, so instead I wrote a new function `updateIfNotNull()` (shown below) which takes the name of the field and the value to change, and returns a string containing the relevant string for the SQL query.
```Python
# updateIfNotNull(FieldName: str, change):
# contains the string to update 'Field' to a new entry if the given `change`` is non-empty.
# >> added another check condition
def updateIfNotNull(FieldName: str, change):
    if change is not None and change != "":
        # >> wrapped in single quotes if string
        if isinstance(change, str):
            return f"{FieldName} = '{change}'"
        return f"{FieldName} = {change}"
    else:
        return ""

# uINN(FieldName: str, change):
# alias for updateIfNotNull
def uINN(FieldName: str, change):
    return updateIfNotNull(FieldName, change)
```
This made it so each update function could just call `uINN()` for each field rather than hardcoding the conditionals (example from `updateMissing.py`):
```Python
cur.execute("UPDATE missing SET " +
    uINN("Date_Missing", Date_Missing) + ", " + 
    uINN("Date_Found", Date_Found) + ", " +
    uINN("Item_ID", Item_ID) + ", " +
    uINN("Description", Description) +
    " WHERE ID = " + str(ID))
```
This allowed for the update functions to be written much faster and also made them easier to edit since the code was more readable.

# Medium-scale Architecture
I did most of the back-end programming for the project (alongside Collin, who helped primarily with CSV conversions both from the old system as well as exporting from the new system). Consequently, I wrote all of the add/update/delete functions for each table, and was the primary developer responsible for maintaining them.

For these components, I used Python with the `sqlite3` library as the primary tools for my part of the project. The `os`, `sys`, and `datetime` libraries were also used as-needed for some of the functions I wrote.

# Domain-specific Architecture
Since we're using SQL to manage a database and Python for the actual back-end, functions had to be written with the restriction in mind that SQL queries done through the `sqlite3` package are handled via SQL queries written as strings-- this meant that, for example, `updateIfNotNull()` had to be written since we needed an easy way to convert the necessary values into the strings in the format desired by SQL.

Likewise, there are a few different areas (particularly in server.py) where SQL queries are first stored in a variable as a multi-line string before being called for the actual SQL query in order to make the code more readable, which it certainly does.

# Security
The average user can only perform `GET` calls from the API and utilize filters to sort the data on the front-end, so their access is severely limited in this way. As such, the primary security concerns revolve around admin access and data sanitization. More specifically, if a threat actor were to introduce bad data into the tables or execute arbitrary SQL queries, that would be very bad!

As such, we make sure that every input that the user can make is sanitized and we only use `cursor.execute()` when calling SQL queries, since that only supports a single query (thus limiting the scope of a potential attack).

On the login side of things, I implemented simple hashing to make sure that the admin password (and user passwords, if they are ever implemented) is never stored anywhere in plain-text, including while the password is changed. This is also instantly more secure than the old system, which does not allow for password changes.