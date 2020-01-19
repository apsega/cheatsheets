# lsof

To list all files opened by a specific user:

```bash
lsof -u root | wc -l
```

Number of files on a host that’s opened by all other users except root:

```bash
lsof -u^root | wc -l
```

To select all Unix Domain Socket files, use `-U`:

```bash
lsof -U | head -10
```

To see the first 15 files held open by all Python processes running on a given host:

```bash
lsof -cpython | head -15
```

List of files held open by the non-Python2.7 processes:

```bash
lsof -cpython -c^python2.7 | head -10
```

Search for all open instances of any directory and its top level files and directories:

```bash
lsof +d /usr/bin | head -4
```

Lists all files held open by a given pid:

```bash
lsof -p $PID
```

Look at the TCP connection program has open:

```bash
lsof -i -a -u $USER | grep $PROGRAM
```

Look at open UDP connections:

```bash
lsof -iUDP
```

via [@copyconstruct](https://medium.com/@copyconstruct/lsof-f2b224eee7b5#.mim72ig4f)

[Back to main](README.md)

