# mcmmo-builds

[![Build](https://github.com/dubsector/mcmmo-builds/actions/workflows/build.yml/badge.svg)](https://github.com/dubsector/mcmmo-builds/actions/workflows/build.yml)
[![Zizmor](https://github.com/dubsector/mcmmo-builds/actions/workflows/zizmor.yml/badge.svg)](https://github.com/dubsector/mcmmo-builds/actions/workflows/zizmor.yml)
[![OpenSSF Scorecard](https://api.securityscorecards.dev/projects/github.com/dubsector/mcmmo-builds/badge)](https://securityscorecards.dev/viewer/?uri=github.com/dubsector/mcmmo-builds)
[![Security Policy](https://img.shields.io/badge/Security-Policy-green)](SECURITY.md)
[![Dependabot](https://img.shields.io/badge/Dependabot-enabled-025E8C?logo=dependabot)](https://github.com/dubsector/mcmmo-builds/network/updates)

Automated daily builds of [mcMMO](https://github.com/mcMMO-Dev/mcMMO) compiled from source.

**Download:** https://dubsector.github.io/mcmmo-builds/

## How it works

1. **Check** — polls upstream master daily for new commits
2. **Build** — compiles from source using the Java version declared in the upstream `pom.xml`
3. **Smoke test** — spins up a Paper and Folia server (latest stable builds, Java version auto-detected from the server JAR) and verifies mcMMO loads without errors
4. **Publish** — only if both smoke tests pass; release includes compatible MC version range

Each release is tagged `build-{short_sha}` and includes the compiled `mcMMO-{version}+{sha}.jar`.

## Verifying releases

Every JAR is signed with [Sigstore](https://sigstore.dev) and includes a [SLSA provenance attestation](https://slsa.dev). You can verify before using:

```sh
# Verify SLSA provenance attestation via GitHub CLI
gh attestation verify mcMMO-<version>+<sha>.jar --repo dubsector/mcmmo-builds

# Verify cosign bundle
cosign verify-blob mcMMO-<version>+<sha>.jar   --bundle mcMMO-<version>+<sha>.jar.sigstore.json
```

Both the `.sigstore.json` bundle and `.intoto.jsonl` provenance file are attached to every release.

## Security

- Workflow YAML is scanned on every push with [zizmor](https://docs.zizmor.sh) — view reports under **Security → Code scanning**
- All GitHub Actions are pinned to exact commit SHAs
- Least-privilege permissions on every job (`permissions: {}` at workflow level)
- Dependencies kept current via [Dependabot](https://docs.github.com/en/code-security/dependabot)
- Supply chain posture tracked by [OpenSSF Scorecard](https://securityscorecards.dev/viewer/?uri=github.com/dubsector/mcmmo-builds)

To report a security issue see [SECURITY.md](SECURITY.md).

## License

This repository contains build automation scripts for mcMMO. The compiled binaries distributed here are derived from [mcMMO](https://github.com/mcMMO-Dev/mcMMO), copyright the mcMMO-Dev contributors, and are distributed under the terms of the [GNU General Public License v3](LICENSE).
