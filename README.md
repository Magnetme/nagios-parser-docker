# nagios-parser-docker

In order to read the status of our nagios servers, we use the following script, which runs within Docker.

This prevents us having to pollute our servers with specific versions of node for just this tool. Effectively the container runs as a script.

You can start it as follows `docker run -v /var/cache/nagios3/:/opt/nagios magnetme/nagios-parser-docker:latest`.
In our case we simply pipe the resulting data through [`jq`](https://stedolan.github.io/jq/) in order to parse some information.

An example to determine whether notifications are inadvertently switched off, one can use the following code

```bash
docker run \
    -v /var/cache/nagios3/:/opt/nagios \
    magnetme/nagios-parser-docker:latest \
    | jq .programstatus[].enable_notifications
```
