# Calendly OAuth callback for mobile development

Temporary HTTPS callback bridge for Calendly's official MCP server.

## Addresses

- OAuth redirect URI: `https://jjmao.github.io/calendly-oauth-callback/`
- Fixed App callback: `autoclaw://connector/calendly`

Register the exact HTTPS URI, including the trailing slash. The Worker must use
that same URI for dynamic registration, authorization and token exchange.

## Behavior

The page receives either `code/state` or `error/state`, clears the query from the
browser address bar, and attempts to open the fixed App callback. A return button
remains available when automatic opening is blocked. Malformed, missing-state or
duplicate result parameters do not open the App. Query-supplied redirect targets
are ignored.

The page uses no third-party assets, analytics, persistent storage or token
exchange. Never commit actual OAuth codes, states, tokens or credentials here.

The App still needs to validate its current authorization attempt and state,
reconstruct the original HTTPS callback URL, and submit it to the authenticated
Worker callback endpoint. Reaching this page does not prove a successful
connection. This repository does not implement the App or Worker changes.

## GitHub Pages

Publish the `main` branch at `/ (root)` using GitHub Pages. GitHub supplies HTTPS.
This is a development callback; move to a team-managed domain for production and
validate the new exact redirect URI through registration and authorization.

## Reference

[Calendly official MCP documentation](https://developer.calendly.com/docs/mcp/calendly-mcp-server)
