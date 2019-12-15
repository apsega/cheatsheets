# Interacting with Kubernetes API

## API to scale

```bash
curl  -X PUT \
      -H "Content-type: application/json" \
      -d '{"kind":"Scale","apiVersion":"extensions/v1beta1","metadata":{"name":"myfirstreplicaset","namespace":"myproject"},"spec":{"replicas":5}}' \
      localhost:8001/apis/extensions/v1beta1/namespaces/myproject/replicasets/myfirstreplicaset/scale
```

```bash
curl -X GET http://localhost:8001/apis/extensions/v1beta1/namespaces/myproject/replicasets/myfirstreplicaset/status
```

[Back to main](../README.md)