# stages

The `stages` configuration is the most important part of the stackmate configuration file, since it contains all of your environments and services that are related to it. The structure of the object is as follows:

```
stages:
  <stage name>:
    <service name>:
      ... service configuration ...
  <other stage name>:
    ....
```

As you can see, each stage is added as a key to the `stages` object and every service that should be deployed on every stage, should be a key to the corresponding stage.

### Service configuration

Every service should have a unique name and can be described with the following attributes:

* `type` - **required** - The service's type. It should be one of the services available
* `region` - the region to deploy the service. If not provided, the default configuration for the project's [`region`](region.md) is used.
* `links` - A list of services that are inter-connected. For example a `mysql` service could be linked to the `application` service in order to allow incoming connections from the `application` service.
* `profile` - A pre-made profile to use for the service. If not specified, the `default` profile is used for the service. You need to refer to every service separately in order to view the corresponding options available.
* `overrides` - An object with attributes to override the default profile with. Each service has its own profile and own overrides. You need to refer to every service separately in order to view the corresponding options available.

These configuration options are available across all services on stackmate, and each service may or may not provide additional attributes to be configured by.

### Reserved keys

To save you time and prevent duplication, we introduced two special keys available in services that would allow you to copy stages in one-another or skip certain services when you copy stages.

* `from` - Specifies the stage to copy from. It should be the name of a stage available in the configuration file.
* `skip` - Specifies the services to skip when copying the stage. It should be a list of valid service names, available in the source stage.

### Example

{% code title=".stackmate/config.yaml" %}
```yaml
name: my-awesome-project
provider: aws
region: eu-central-1
...
stages:
  production:    # the production stage
    mysqldb:        # a mysql database service
      type: mysql
      size: db.t3.micro
      storage: 30
      # ....
    postgresqldb:   # a postgresql database service
      type: postgresql
      size: db.t3.micro
      storage: 30
      # ...

  uat:            # the uat stage, copied from production, not skipping anything
    from: production
    
  staging:        # the staging stage, copied from production
    from: production    # we specify the source stage
    skip:               # we specify the services to skip
      - postgresqldb        # we're skipping the postgresql service on staging
```
{% endcode %}
