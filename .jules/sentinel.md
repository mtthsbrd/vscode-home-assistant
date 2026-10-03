## 2025-02-14 - Prevent Token Leakage in Axios Errors
**Vulnerability:** Axios errors contain the full request configuration in the `config` property, which includes all HTTP headers. When catching API call failures and logging or stringifying the full error object, the sensitive `Authorization: Bearer <token>` header was being leaked into logs and potential output.
**Learning:** Raw errors thrown by HTTP clients (like Axios) are not safe to log directly because they encapsulate sensitive request details.
**Prevention:** Always log specific, safe properties of the error object (like `error.message`) instead of the entire object, or manually redact sensitive headers from the `error.config.headers` before logging.
