# **SQL injection**
- `SQL injection` happens when we let users input data that needs to be used in SQL statement and we don't escape any special characters
- is probably one of the most common ways that "hackers" will attempt to attack our website
- some `SQL injection` attacks can be used to gain data, a large chunk of them will simply destory a large portion of our data, leaving us with an empty database
- for example, create a SQL statement using the following code is a very bad idea, because the following code doesn't know anything about SQL, so all they know how to do is to combine strings together, meaning if a user were to enter a value with nefarious intent, it could easily create an SQL statement that doesn't do what we intended
```golang
func buildSql(email string) string {
    return fmt.Sprintf("SELECT * FROM users WHERE email='%s';", email)
}
```
- consider the example above, what happens if a user attempts to sign in using an email address like `; DROP TABLE user;`, we should see a SQL statement that looks like the following:
```SQL
SELECT * FROM users WHERE email='', DROP TABLE users;'';
```
- it will add an extra SQL statement to the end that **DROPS THE ENTIRE USERS TABLE!**
- by using package/modules such as `database/sql` package to create our SQL statements, we get a free layer of protection against this, as the `package/sql` package is aware of all special characters, so when we try to insert a string with a single quote `(')` into a statement being constructed by the `database/sql` package it will escape the special characters and prevent any nefarious SQL statements from ever being executed