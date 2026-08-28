# release-please-test

A tiny Go program used to learn [Release Please](https://github.com/googleapis/release-please), Google's open-source release-PR automation tool.

## Run it

```sh
go run .
go test ./...
```

The module targets Go 1.27, matching the installed toolchain.

## Release Please

The GitHub Actions workflow in `.github/workflows/release-please.yml` runs whenever a commit lands on `master` (and can also be started manually). It uses the configuration in `release-please-config.json`, writes release notes to `CHANGELOG.md`, and tracks the current released version in `.release-please-manifest.json`.

Release Please reads [Conventional Commit](https://www.conventionalcommits.org/) messages:

| Commit message | Expected release change |
| --- | --- |
| `fix: correct greeting punctuation` | patch |
| `feat: add a language option` | minor |
| `feat!: change greeting output` | major |
| `docs: clarify setup` | no release |

To try it out:

1. Push this setup to `master`.
2. Merge a conventional commit such as `feat: add an enthusiastic greeting`.
3. The workflow opens or updates a release PR with a generated changelog and version bump.
4. Merge that release PR. The workflow creates the GitHub release and tag.

The initial manifest version is `0.1.0`; it represents the version Release Please will bump from. This example does not embed a runtime application version, which keeps the Go program intentionally minimal.
