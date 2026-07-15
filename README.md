## Megaspell Server Registry ##

Simple service that game uses to discover online servers.

### Key features ###

- Persistent and supports instancing.
- Servers should regularly send keepalive requests to avoid being removed from online registry.
- Host-based trust - host can only register its own servers.  
  **Important:** registry is validating host by using X-Real-IP header. Load balancer should be configured
  to set this header.

### Deployment in container ###

Required environment properties:

- `DATABASE_URL` - example `jdbc:postgresql://example.com:5432/postgres`
- `DATABASE_USER`
- `DATABASE_PASSWORD`

Example compose configuration:

```yaml
megaspell-server-registry:
  image: ghcr.io/pipbuckstudio/megaspell-server-registry:latest
  restart: unless-stopped
  ports:
    - "8080:8080"
  environment:
    DATABASE_URL: jdbc:postgresql://example.com:5432/postgres
    DATABASE_USER: postgres
    DATABASE_PASSWORD: "${POSTGRES_PASSWORD}"
  volumes:
    - postgres-data:/var/lib/postgresql/data
```

---

Forked from [Megaspell/MegaspellLauncher](https://github.com/Megaspell/MegaspellServerRegistry)
