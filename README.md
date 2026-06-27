# mcmmo-builds

Automated daily builds of [mcMMO](https://github.com/mcMMO-Dev/mcMMO) compiled from source.

Builds run daily and publish a new release whenever upstream master changes. Each release is tagged `build-{short_sha}` and includes the compiled `mcMMO-{version}+{sha}.jar`.

## Security

The workflow is scanned on every push with [zizmor](https://docs.zizmor.sh). You can view the latest report under the **Security → Code scanning** tab of this repo.
