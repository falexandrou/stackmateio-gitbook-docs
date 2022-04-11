# stackmate stage

The `stackmate stage` command copies a stage and adds it to the configuration file.

### Usage

```
stackmate stage <stage> --from <source> [...arguments]
```

### Arguments

* `<stage>` should be the name of the stage to add and it should not already be present on your `.stackmate/config.yml` file

### Options

* `--from <source>` - **required** - Where to base the stage from. It should be one of the stages that are already available in your `.stackmate/config.yml` file
* `--skip service1, service2` - Comma separated list of the services to skip when inheriting from the base stage. For example, you can base the new stage onto `production` but choose to skip the `cache` service
