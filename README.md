# Openstack Integration Pack

StackStorm pack for OpenStack integration.

## Configuration

Pack configuration requires to URLs and of the openstack APIs and an authetication mechanism. There are two way to supply this information :

### Token based

Supply an already acquired token and a URL pointing to the service API. Both of these would have to be acquired from the service catalog.

To acquire a token -

```
curl -s -X POST $OS_AUTH_URL/tokens -H "Content-Type: application/json" -d '{"auth": {"tenantName": "'"$OS_TENANT_NAME"'", "passwordCredentials": {"username": "'"$OS_USERNAME"'", "password": "'"$OS_PASSWORD"'"}}}' | python -m json.tool
```
See the [OpenStack manual](http://docs.openstack.org/api/quick-start/content/index.html#authenticate) for more information on above command.

```yaml
---
token:
    OS_TOKEN: "xxxxxxxxxxxxxxxxxxxx"
    OS_URL: "http://{API_IP}:{API_PORT}/v2/{TENANT_ID}"
```

### Password based

Tokens are ephemeral and typical expiry is short; in those cases it might be preferred to use the password based approach.

```yaml
---
password:
    OS_AUTH_URL: # authentication url
    OS_TENANT_ID: # id of the tenant
    OS_TENANT_NAME: # name of the tenant
    OS_USERNAME: # username
    OS_PASSWORD: # password
```

## Actions

### Autogenerating actions

All(?) actions in this pack are autogenerated. The is a custom [autogen](/etc/autogen.py) that is used for this purpose.

```
usage: autogen.py [-h] [--ns NAMESPACE] [--path BASE_PATH] [--debug]

optional arguments:
  -h, --help            show this help message and exit
  --ns NAMESPACE, -n NAMESPACE
  --path BASE_PATH, -p BASE_PATH
  --debug, -d
```

NAMESPACE - namespace of the command to generate e.g. 'server' or 'server create'
BASE_PATH - the location where to write the action metadata
debug - will spit out extra debug information

## Sensors

No sensors in this pack.

