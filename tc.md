# Linux traffic control utility `tc`

## Latency and jitter

delay packets for 10ms:
```bash
tc qdisc add dev eth0 root netem delay 10ms
```

Remove any inserted noise/delays, etc.:

```bash
tc qdisc rem dev eth0 root
```

delay packets with value from uniform [90ms-110ms] distribution:
```bash
tc qdisc add dev eth0 root netem delay 100ms 10ms
```

delay packets with value from uniform [90ms-110ms] distribution and 25% correlated with value of previous packet
```bash
tc qdisc add dev eth0 root netem delay 100ms 10ms 25%
```

delay packets with value from normal distribution (mean 100ms, jitter 10ms):
```bash
tc qdisc add dev eth0 root netem delay 100ms 10ms distribution normal
```

delay packets with value from normal distribution (mean 100ms, jitter 10ms) and 25% correlated with value of previous packet:
```bash
tc qdisc add dev eth0 root netem delay 100ms 10ms 25% distribution normal
```

## Packet loss

drop packets randomly with probability of 0.1%:
```bash
tc qdisc add dev eth0 root netem loss 0.1%
```

drop packets randomly with probability of 0.3% and 25% correlated with drop decision for previous packet:
```bash
tc qdisc add dev eth0 root netem loss 0.3% 25%
```

[Back to main](README.md)