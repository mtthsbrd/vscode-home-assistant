## 2026-10-04 - [Fix Axios error object logging in haConnection]
**Vulnerability:** The system previously logged full Axios error objects on failed `callApi` and `callService` requests. This resulted in leaking sensitive information since Axios attaches the original request configuration (which includes the `Authorization` header with the Home Assistant access token) to the error object at `error.config`.
**Learning:** Even internal VS Code extension output logs can become a source of credential leakage if error objects containing request configurations are fully serialized and dumped into the console.
**Prevention:** Rather than logging the full error object, only properties specifically meant for debugging like `error.message` should be logged to prevent inadvertent data exposure.

## 2026-10-04 - [Generate Schemas path resolution fix]
**Vulnerability:** N/A (Build fix)
**Learning:** The schema generation script (`src/language-service/src/schemas/generateSchemas.ts`) failed when running after compilation because `__dirname` resolves to `dist/schemas` during execution, whereas the mapped `.ts` files remain in `src/schemas`.
**Prevention:** Determine if execution context is within `dist`, and if so, dynamically resolve `srcSchemasPath` by walking up the directory tree and then down to `src/schemas`.
