# IDE Services REST API

## Discover
- OpenAPI JSON: `https://<server>/api-docs`
- Swagger UI: `https://<server>/swagger-ui/index.html`

## Auth — pick one

A. **Browser JWT** (quick, expires). Extract from the SPA's localStorage in an authenticated session:
```js
JSON.parse(localStorage.getItem('TOKENS_V2')).accessToken
```
Send as: `Authorization: Bearer <token>`

B. **Automation token** (stable). Create in UI → Configuration → Automation Tokens, or POST `/api/automation-tokens`. Send as: `Authorization: Automation <token>`
