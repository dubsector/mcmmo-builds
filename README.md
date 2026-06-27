# mcmmo-builds

Automated daily builds of [mcMMO](https://github.com/mcMMO-Dev/mcMMO) compiled from source.

## How it works

1. **Check** — polls upstream master daily for new commits
2. **Build** — compiles from source using the Java version declared in the upstream `pom.xml`
3. **Smoke test** — spins up a Paper and Folia server (latest stable builds, Java version auto-detected from the server JAR) and verifies mcMMO loads without errors
4. **Publish** — only if both smoke tests pass; release includes compatible MC version range

Each release is tagged `build-{short_sha}` and includes the compiled `mcMMO-{version}+{sha}.jar`.

## Security

The workflow is scanned on every push with [zizmor](https://docs.zizmor.sh). You can view the latest report under the **Security → Code scanning** tab of this repo.
