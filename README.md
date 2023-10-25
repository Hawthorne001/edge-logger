# Baselime Edge Logger

OpenTelemetry aware logger for Cloudflare Workers and Vercel Edge Functions.

## Usage

```bash
npm i @baselime/edge-logger
```

### Usage

```typescript
import { BaselimeLogger } from '@baselime/edge-logger'

export interface Env {
	BASELIME_KEY: string
}

export default {
	async fetch(req: Request, env: Env, ctx: ExecutionContext): Promise<Response> {
		const logger = new BaselimeLogger({
			ctx,
			apiKey: env.BASELIME_KEY,
			service: 'my-worker',
			dataset: 'cloudflare',
			namespace: 'fetch',
			requestId: crypto.randomUUID(),
		})

		logger.info('Hello world', { cfRay: req.headers.get('cf-ray'), foo: 'bar' })

		ctx.waitUntil(logger.flush());
		return new Response('Hello world!');
	}
}
```

## Supported methods

```javascript
logger.info("This is an informational message", { payload: { foo: "bar" } });
logger.warn("This is a warning message", { payload: { foo: "bar" } });
logger.error("This is an error message", { payload: { foo: "bar" } });
```

### Contributing

If you would like to contribute to the development of this library, please
submit a pull request on GitHub.

### License

This library is licensed under the MIT License. See the [LICENSE](LICENSE) file
for details.

<!-- Badges -->

[docs]: https://baselime.io/docs/
[docs_badge]: https://img.shields.io/badge/docs-reference-blue.svg?style=flat-square
[license]: https://opensource.org/licenses/MIT
[license_badge]: https://img.shields.io/github/license/baselime/lambda-logger.svg?color=blue&style=flat-square&ghcache=unused