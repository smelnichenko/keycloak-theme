# Keycloak Theme

Custom Keycloak theme (PatternFly 5, dark gradient) for the schnappy realm. Also used as the Keycloak container image with realm import.

## Structure

```
themes/schnappy/       # Theme files (login, account)
Dockerfile             # Keycloak image + theme + realm import support
```

## Build

```bash
docker build -t git.pmon.dev/schnappy/keycloak-theme:latest .
```

The Dockerfile extends the official Keycloak image, copies the theme, and supports `--import-realm` via init container that templates secrets into the realm JSON.

## Full Infrastructure Docs

See `schnappy/ops` repo `CLAUDE.md` for complete infrastructure documentation.
