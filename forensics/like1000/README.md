# forensics / like1000

> Points: 250

## Question

> This [.tar file](1000.tar) got tarred alot. Also available at /problems/like1000_0_369bbdba2af17750ddf10cc415672f1c.

### Hint

> Try and script this, it'll save you alot of time

## Solution

We get a good look at what we're being asked to do by simply listing the files in `1000.tar`.

```console
$ tar -tf 1000.tar
999.tar
filler.txt
```

Assuming this goes down to `1.tar`, we can use a bash script.

```bash
for i in `seq 1000 -1 2`;
do
  tar -xf "$i.tar" "$(($i - 1)).tar"
  rm "$i.tar"
done
```

Looking into `1.tar`, we find the flag. Extract `flag.png` for an image of the flag.

```console
$ tar -tf 1.tar
flag.png
filler.txt
$ tar -xf 1.tar flag.png
```

### Flag

`picoCTF{l0t5_0f_TAR5}`
