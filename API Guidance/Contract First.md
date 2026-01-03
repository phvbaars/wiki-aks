## OpenAPI-first generators 

Best practice:
Generate APIs from a contract (strongly recommended).

```
Bash:
openapi-generator generate \
  -i openapi.yaml \
  -g nodejs-express-server
```

Generate:
- Server stubs
- Dockerfiles
- Clients

