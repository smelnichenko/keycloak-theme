# keycloak-theme

Custom Keycloak login/account theme for the `schnappy` realm — PatternFly 5 base with a dark-gradient skin matching pmon.dev. Packaged as a Keycloak container image so the bare-metal Keycloak on the Pis (and the in-cluster test Keycloak in `schnappy-auth`) can mount it without a separate volume.

## Base image

`quay.io/keycloak/keycloak:26.5.6` + `themes/schnappy/`.

## Theme

```
themes/schnappy/login/
  theme.properties              # parent=keycloak.v2, dark-mode enabled, custom CSS layered after PatternFly
  resources/css/schnappy.css    # the actual brand styling
```

`theme.properties` extends the v2 login theme and adds `schnappy.css` after the upstream PatternFly stylesheets so brand overrides win without forking templates.

## Usage

Built by Woodpecker CI and pushed to `git.pmon.dev/schnappy/keycloak-theme`. Production Keycloak runs the resulting image directly; the `schnappy-auth` chart pulls the same image for Vagrant E2E. The realm sets `loginTheme: schnappy`.

To preview locally:

```bash
docker build -t keycloak-theme:dev .
docker run --rm -p 8080:8080 \
  -e KEYCLOAK_ADMIN=admin -e KEYCLOAK_ADMIN_PASSWORD=admin \
  keycloak-theme:dev start-dev
```

Then create or import a realm and set its login theme to `schnappy`.
