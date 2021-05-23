```
logstash-7.12.1/bin/logstash -e "input { stdin { } } output { stdout { } }"
logstash-7.12.1/bin/logstash -f elk-files/config/pipeline.conf
logstash-7.12.1/bin/logstash -f elk-files/config/pipeline.conf --config.reload.automatic
```

```
filter {
    grok {
        match => { "message" => "%{IP:ip_address} %{USER:identity} %{USER:auth} \[%{HTTPDATE:req_ts}\] \"%{WORD:http_verb} %{URIPATHPARAM:req_path} HTTP/%{NUMBER:http_version}\" %{INT:http_status:int} %{INT:num_bytes:int}" }
    }
}
```
