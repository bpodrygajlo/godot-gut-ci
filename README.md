# Godot GUT CI

This [GitHub action](https://github.com/features/actions) allows you to run your [Godot GUT tests](https://github.com/bitwes/Gut), 
so you can make sure nothing is broken :).

## How to use

Create a folder called `.github/workflows` in the root project folder.
Then create a yaml file to configure your tests, for example `godot-tests.yml`.

### Yaml content

Copy and paste the following content in your yaml file:

```yaml
name: "godot gut test"
on: push

jobs:
  execute-gut:
    name: Run GUT tests
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v2

      - name: Docker test
        uses: ceceppa/godot-gut-ci@master
```

### With

Some action parameter can be customised using the `with` property:

|parameter|description|default|
|---|---|---|
|godot_version|The godot version you want to use to run your tests|3.2.2|
|unit_test|The godot resource folder containing your unit tests|res://tests/unit|
|integration_test|The godot resource folder containing your integration tests||
|output_file|Name of the output file. Outputs to stdout if not specified||

**NOTE**: If you're customising `unit_test` or `integration_test`, don't forget to specify the `res://` prefix.

#### Example

```yaml
name: "godot gut test"
on: push

jobs:
  execute-gut:
    name: Run GUT tests
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v2
      - name: Docker test
        uses: ceceppa/godot-gut-ci@master
        with:
          godot_version: 3.2.1 # uses godot 3.2.1
          integration_test: res://tests/integration # specify the path for the integration tests
```
