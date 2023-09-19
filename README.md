# owasp-zap
owasp-zap

run docker container
```sh
docker run -d -v $(pwd):/zap/wrk/:rw -u zap -p 8080:8080 -i owasp/zap2docker-weekly zap-x.sh -daemon -host 0.0.0.0 -port 8080 -config 'api.addrs.addr.name=.*' -config 'api.addrs.addr.regex=true' -config 'api.key=12345'
```

add URL
```sh
curl -s "http://localhost:8080/JSON/core/action/accessUrl/?apikey=12345&url=https://www.webscantest.com&followRedirects=false" | jq .
```

list all sites
```sh
curl -s "http://localhost:8080/JSON/core/view/sites/?apikey=12345" | jq .
```

list all hosts
```sh
curl -s "http://localhost:8080/JSON/core/view/hosts/?apikey=12345" | jq .
```

list all httpSession sites
```sh
curl -s "http://localhost:8080/JSON/httpSessions/view/sites/?apikey=12345" | jq .
```

create new httpSession
```sh
curl -s "http://localhost:8080/JSON/httpSessions/action/createEmptySession/?apikey=12345&site=www.webscantest.com:443&session=session1" | jq .
```

show active httpSession
```sh
curl -s "http://localhost:8080/JSON/httpSessions/view/activeSession/?apikey=12345&site=www.webscantest.com:443" | jq .
```

start spider scan
```sh
curl -s "http://localhost:8080/JSON/spider/action/scan/?apikey=12345&zapapiformat=JSON&formMethod=GET&url=https://www.webscantest.com"
```

show spider scan status
```sh
curl -s "http://localhost:8080/JSON/spider/view/status/?apikey=12345" | jq .
```


list all context
```sh
curl -s "http://localhost:8080/JSON/context/view/contextList/?apikey=12345" | jq .
```

create context
```sh
curl -s "http://localhost:8080/JSON/context/action/newContext/?apikey=12345&contextName=Default+Context" | jq .
```

show specific context
```sh
curl -s "http://localhost:8080/JSON/context/view/context/?apikey=12345&contextName=Default+Context" | jq .
```

add regex into includeInContext
```sh
curl -s "http://localhost:8080/JSON/context/action/includeInContext/?apikey=12345&contextName=Default+Context&ex=https://www.webscantest.com.*" | jq .
```

list all includeRegexs
```sh
curl -s "http://localhost:8080/JSON/context/view/includeRegexs/?apikey=12345&contextName=Default+Context" | jq .
```

start active scan
```sh
curl -s "http://localhost:8080/JSON/ascan/action/scan/?apikey=12345&zapapiformat=JSON&formMethod=GET&url=https://www.webscantest.com&recurse=&inScopeOnly=false&scanPolicyName=&method=&postData=&contextId="
```

show active scan status
```sh
curl -s "http://localhost:8080/JSON/ascan/view/status/?apikey=12345" | jq .
```

list alert counts by url
```sh
curl -s "http://localhost:8080/JSON/alert/view/alertCountsByRisk/?apikey=12345&url=https://www.webscantest.com&recurse=True" | jq .
```

list alerts by risk
```sh
curl -s "http://localhost:8080/JSON/alert/view/alertsByRisk/?apikey=12345&url=https://www.webscantest.com&recurse=True" | jq .
```

show json report
```sh
curl -s "http://localhost:8080/OTHER/core/other/jsonreport/?apikey=12345" | jq .
```

list all alerts
```sh
curl -s "http://localhost:8080/JSON/core/view/alerts/?apikey=12345" | jq .
```

shutdown
```sh
curl -s "http://localhost:8080/JSON/core/action/shutdown/?apikey=12345"
```
