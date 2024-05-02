# Log

## General

何を出力すべきか？(TODO)

## Tool

### 転送・集約

#### syslog

log を転送することができる。OS 標準で入っていることが多いので、Docker の Host サーバー等、わざわざ依存を増やしたくないケースには便利に見える。

#### fluentd

log の転送・集約ができる。plugin で、種々の形式の log をパースして望ましい形に加工して保存等が可能。また、保存先も plugin が豊富。log の集約サーバーを設ける場合、あるいは S3 等に log を転送したい場合に利用か？

#### fluentbit

fluentd の発展系。高速かつ、Ruby に依存してないので管理面は楽に見えるが、plugin は少ない。

## Practice

### Docker (Self Hosting)

標準では、log-driver として、`json-file`が利用される STDOUT, ERR の出力は、[docker logs](https://docs.docker.com/reference/cli/docker/container/logs/)で確認可能。log の保管先は、[docker inspect --format='{{.LogPath}}' $INSTANCE_ID](https://docs.docker.com/reference/cli/docker/inspect/#get-an-instances-log-path)で取得できる。標準の`json-file`は、`max-size`が unlimited なので、docker run 時に、log rotation の設定をした方が良い。

真っ当に運用を行うのであれば、log-driver として、syslog / fluentd を指定するのがより望ましく思える。
