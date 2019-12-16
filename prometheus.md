# prometheus

### deleting metrics

```bash
curl -XDELETE -g 'http://localhost:9090/api/v1/series?match[]={job="script-exporter",script=~"ea-script"}'
```

[Back to main](README.md)