# tcpdump

## headers

```bash
stdbuf -oL -eL /usr/sbin/tcpdump -A -s 10240 "tcp port 80 and (((ip[2:2] - ((ip[0]&0xf)<<2)) - ((tcp[12]&0xf0)>>2)) != 0)" | egrep -a --line-buffered ".+(GET |HTTP\/|POST )|^[A-Za-z0-9-]+: " | perl -nle 'BEGIN{$|=1} { s/.*?(GET |HTTP\/[0-9.]* |POST )/\n$1/g; print }'
```

[Back to main](README.md)