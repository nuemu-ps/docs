# Log

## General

何を出力すべきか？(TODO)

## Tool

### syslog

「入門　監視」で推奨されている。log を転送して集約するのに便利？(TODO)

### fluentd

syslog よりモダンに、log の転送・集約ができる？(TODO)

## Practice

### Docker (Self Hosting)

標準では、log-driver として、`json-file`が利用される STDOUT, ERR の出力は、[docker logs](https://docs.docker.com/reference/cli/docker/container/logs/)で確認可能。log の保管先は、[docker inspect --format='{{.LogPath}}' $INSTANCE_ID](https://docs.docker.com/reference/cli/docker/inspect/#get-an-instances-log-path)で取得できる。標準の`json-file`は、`max-size`が unlimited なので、docker run 時に、log rotation の設定をした方が良い。

真っ当に運用を行うのであれば、log-driver として、fluentd / syslog を指定するのがより望ましく思える。
