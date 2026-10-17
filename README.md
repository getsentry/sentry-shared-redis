# sentry-shared-redis

Shared Redis for Sentry developer environments, run by [devservices](https://github.com/getsentry/devservices). Repos such as `getsentry/sentry`, `getsentry/snuba`, and `getsentry/relay` depend on it, so their services share one Redis container.

## Add it to your service

1. Add a remote dependency to your repo's `devservices/config.yml`:

   ```yaml
   x-sentry-service-config:
     dependencies:
       redis:
         description: Shared Redis
         remote:
           repo_name: sentry-shared-redis
           branch: main
           repo_link: https://github.com/getsentry/sentry-shared-redis.git
   ```

2. Add `redis` to each mode in `modes` that needs it.
3. Run `devservices up`. devservices fetches this repo and starts the container.

## What you get

- Redis 5.0 from `ghcr.io/getsentry/image-mirror-library-redis:5.0-alpine`, listening on `127.0.0.1:6379`.
- Data that persists across restarts in the `redis-data` Docker volume, with the append-only file enabled.
- A container on the `devservices` Docker network.

The full definition is in [`devservices/config.yml`](devservices/config.yml).
