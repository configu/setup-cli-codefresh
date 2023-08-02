# configu/setup-cli-codefresh

[![pipeline status](https://gitlab.com/configu1/setup-cli-gitlab-ci/badges/main/pipeline.svg)](https://gitlab.com/configu1/setup-cli-gitlab-ci/-/commits/main) [![Latest Release](https://gitlab.com/configu1/setup-cli-gitlab-ci/-/badges/release.svg)](https://gitlab.com/configu1/setup-cli-gitlab-ci/-/releases)


The configu/setup-cli-gitlab-ci project contains a .yml template that sets up Configu CLI in your GitLab CI/CD workflow by downloading a specific version of Configu CLI and adding it to the `PATH`.

After you've included and extended the template, subsequent steps in the same job can run arbitrary Configu CLI commands. All of Configu commands work exactly like they do on your local command line.

## Usage

The default configuration installs the latest version of Configu CLI.

```yaml
include:
  - remote: 'https://gitlab.com/configu1/setup-cli-gitlab-ci/-/raw/main/configu.gitlab-ci.yml'

some-job:
  stage: deploy
  extends: .configu/setup-cli
  script:
    - echo "use configu cli here"
```

A specific version of Configu CLI can be installed.

```yaml
some-job:
  stage: deploy
  extends: .configu/setup-cli
  variables:
    version: "0.4.4"
  script:
    - configu --version
```

Credentials for `Configu store` ([app.configu.com](https://app.configu.com/)) can be configured.

1. In your Configu organization, go to Settings > Access Tokens
2. Create a new Access token and copy its value
3. In your GitLab project, go to to Settings > CI/CD > Variables 
4. Create a new CONFIGU_ORG variable with your Configu Organization id
5. Create a new CONFIGU_TOKEN variable with the Access Token value you copied in step 2, make sure to enable "Mask variable" option.

```yaml
some-job:
  stage: deploy
  extends: .configu/setup-cli
  script:
    - configu export --store "configu://-" --set "production" --schema "path/to/schema.cfgu.json"
```

## Variables

The template supports the [following variables](https://gitlab.com/configu1/setup-cli-gitlab-ci/-/blob/main/configu.gitlab-ci.yml#L1).

## License

This orb is licensed under [Apache License 2.0](https://gitlab.com/configu1/setup-cli-gitlab-ci/-/blob/main/LICENSE).

## References
- [Configu SaaS platform (app.configu.com)](https://app.configu.com/)
- [Configu Documentation](https://configu.com/docs)
- [GitLab CI/CD Documentation](https://docs.gitlab.com/ee/ci/)