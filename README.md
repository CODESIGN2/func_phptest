# func_phptest
OpenFaaS PHP7 CLI Test

```shell
git clone https://github.com/CODESIGN2/func_phptest
```

create file `func_phptest.yml` with the following contents (replacing `http://192.168.0.16:8000` with your gateway IP & port)

```yaml
provider:
  name: faas
  gateway: http://192.168.0.16:8080
functions:
  func_phptest:
    lang: Dockerfile
    handler: ./func_phptest
    image: func_phptest

```

run `faas-cli build -f func_phptest.yml` followed by `faas-cli deploy -f func_phptest.yml`
