# configu/setup-cli-codefresh

[![Codefresh build status]( https://g.codefresh.io/api/badges/pipeline/configu/setup-cli-codefresh%2Fsetup-cli-codefresh?type=cf-1&key=eyJhbGciOiJIUzI1NiJ9.NjRjYTlkOTYzNmQzNzJmNzI0ZGVhNjlk.XQdQn6kqcCVdKxS58aZ7W5Xs4EKUOPM4jOffc_FlQbk)]( https://g.codefresh.io/pipelines/edit/new/builds?id=64caa99af66f1518afd38547&pipeline=setup-cli-codefresh&projects=setup-cli-codefresh&projectId=64ca9deacf5a1d0611eed016)

The `configu/setup-cli-codefresh` project contains a `typed plugin` that sets up Configu CLI in your `Codefresh pipelines` workflow by downloading a specific version of Configu CLI and adding it to the `PATH`.

After you've used the plugin, subsequent `commands` in the same `step` can run arbitrary Configu CLI commands.
All of Configu commands work exactly like they do on your local command line.

## Usage

The default configuration installs the latest version of Configu CLI.

```yaml
workflow:
  configu_export:
    title: Export configurations
    type: configu
    arguments:
      COMMANDS:
        - configu --version
        - configu eval --store 'configu' --set 'test/codefresh' --schema '/codefresh/volume/${{CF_REPO_NAME}}/.cfgu.json' | configu export
```

A specific version of Configu CLI can be installed.

```yaml
workflow:
  configu_version:
    title: Install specific version of Configu CLI
    type: configu
    arguments:
      VERSION: 0.12.5
      COMMANDS:
        - configu --version
```

Credentials for `Configu store` ([app.configu.com](https://app.configu.com/)) can be configured.

1. In your `Configu platform organization`, go to `Settings > Access Tokens`
2. Create a `new Access` token and `copy its value`
3. In your `Codefresh project`, go to to `Projects > Settings > Variables`
4. Create a new CONFIGU_ORG variable with your Configu Organization id
5. Create a new CONFIGU_TOKEN variable with the Access Token value you copied in step 2, make sure to enable `"Encrypt Value"`.

<!-- ```yaml
some-job:
  stage: deploy
  extends: .configu/setup-cli
  script:
    - configu export --store "configu://-" --set "production" --schema "path/to/schema.cfgu.json"
``` -->

## Variables

The plugin supports the [following inputs](https://github.com/configu/setup-cli-codefresh/blob/main/configu-step.yml#L34).


## License

This plugin is licensed under [Apache License 2.0](https://gitlab.com/configu1/setup-cli-gitlab-ci/-/blob/main/LICENSE).

## References
- [Configu platform (app.configu.com)](https://app.configu.com/)
- [Configu Documentation](https://configu.com/docs)
- [Codefresh Documentation](https://codefresh.io/docs/)