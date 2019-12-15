# SSH

## Key generation

```bash
    ssh-keygen -t rsa -C "email@addres.com" -b 4096
```

Change password for key:

```bash
    ssh-keygen -p <keyname>
```

Tunnel port through SSH:

```bash
ssh -L 127.0.0.1:5900:127.0.0.1:5900 pi@xxx.xx.xx.xx
```
