# nest-base

Minimal NestJS template for new microservices: Node 24, ESM, zod config and validation, pino structured logging, health checks, a consistent error format, Docker and CI.

## Start a new service

```bash
git clone --depth 1 https://github.com/tuandung1304/nest-base.git my-service
cd my-service
rm -rf .git && git init

# Rename the template (package name, SERVICE_NAME, README title)
sed -i 's/nest-base/my-service/g' package.json .env.example src/config/env.schema.ts README.md     # Linux
sed -i '' 's/nest-base/my-service/g' package.json .env.example src/config/env.schema.ts README.md  # macOS

yarn install
cp .env.example .env
yarn dev
```

## Scripts

| Command                          | Description                      |
| -------------------------------- | -------------------------------- |
| `yarn dev`                       | Start in watch mode              |
| `yarn build` / `yarn start:prod` | Build to `dist/` and run it      |
| `yarn test` / `yarn test:e2e`    | Unit tests / e2e tests (`test/`) |
| `yarn lint` / `yarn fmt`         | oxlint / oxfmt                   |
| `yarn typecheck`                 | TypeScript without emitting      |

Docker: `docker build -t my-service .` then `docker run -p 3000:3000 my-service`.

## Conventions

- Env vars: declare in `src/config/env.schema.ts` and `.env.example`.
- Request DTOs: extend `createZodDto(schema)`, validated globally.
- Errors: throw Nest's `HttpException`s; every error response is `{ statusCode, error, message, requestId, errors? }` (`errors` only for validation). Unexpected errors return a generic 500 and are logged with their stack.
- Health checks: `/health/live`, `/health/ready`. Add dependency indicators (database, cache, ...) to `ready` only.
- Logging: inject `PinoLogger` (`nestjs-pino`) or use Nest's `Logger`. JSON to stdout (pretty in development); every line carries `service` and `requestId` (from/echoed as `x-request-id`).
- Commits: [Conventional Commits](https://www.conventionalcommits.org/), checked by commitlint. Git hooks format, lint and typecheck staged code before commit, and run unit tests before push.
