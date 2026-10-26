# nest-base

Minimal NestJS template for new microservices.

## Getting started

```bash
yarn install
cp .env.example .env
yarn dev
```

## Conventions

- Env vars: declare in `src/config/env.schema.ts` and `.env.example`.
- Request DTOs: extend `createZodDto(schema)`, validated globally.
- Errors: throw Nest's `HttpException`s; every error response is `{ statusCode, error, message, requestId, errors? }` (`errors` only for validation). Unexpected errors return a generic 500 and are logged with their stack.
- Health checks: `/health/live`, `/health/ready`.
- Logging: inject `PinoLogger` (`nestjs-pino`) or use Nest's `Logger`. JSON to stdout (pretty in development); every line carries `service` and `requestId` (from/echoed as `x-request-id`).
- Commits: [Conventional Commits](https://www.conventionalcommits.org/).
