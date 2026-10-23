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
- Health checks: `/health/live`, `/health/ready`.
- Commits: [Conventional Commits](https://www.conventionalcommits.org/).
