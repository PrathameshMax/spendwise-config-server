# spendwise-config-server

Spring Cloud Config server. Serves the YAML in spendwise-config (Git backend) to every service at startup.

| | |
|---|---|
| Port | 8888 |
| Configuration | `config-server*.yml` in [spendwise-config](https://github.com/PrathameshMax/spendwise-config) |
| Shared code | `com.spendwise:spendwise-parent / spendwise-common / spendwise-events` from [spendwise-shared](https://github.com/PrathameshMax/spendwise-shared) |
| Image | `ghcr.io/prathameshmax/spendwise-config-server:<git-sha>` and `:main` |

## Build

Reading the shared packages needs a classic GitHub token with `read:packages` in
`GITHUB_PACKAGES_TOKEN` and a `<server>` with id `github` in `~/.m2/settings.xml`.

```bash
./mvnw -B verify
docker build --secret id=gh_token,env=GITHUB_PACKAGES_TOKEN -t spendwise-config-server .
```

## CI

`.github/workflows/ci.yml`: every pull request builds, tests and builds the image; every push to
`main` also pushes the image to GHCR, tagged with the commit SHA and `main`. The repository secret
`PACKAGES_READ_TOKEN` (classic token, `read:packages`) lets CI read the shared packages.
